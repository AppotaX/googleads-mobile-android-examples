# Tài Liệu kết nối Google Mobile Ads SDK cho Android


Hướng dẫn này sẽ giúp bạn biết làm cách nào để tích hợp Google Mobile Ads SDK vào một ứng dụng mới và sử dụng nó để hiển thị biểu ngữ DoubleClick đơn giản. Nó sẽ cho bạn khoảng ba mươi phút để hoàn thành và sẽ cung cấp cho bạn một cảm giác tốt về các chức năng SDK trong ứng dụng. Nếu bạn chưa quen với Google Mobile Ads,  đây là một nơi tuyệt vời để bắt đầu trước khi chuyển sang các ví dụ nâng cao hơn.

## Điều kiện tiên quyết


 - Đang chạy Android Studio 1.0 hoặc cao hơn
 -  Đang phát triển cho Android cấp 9 hoặc cao hơn
 Để hoàn thành xong hướng dẫn Bắt đầu này, bạn cần cài đặt Android Studio trên thiết bị phát triển của mình. Nếu bạn chưa cài đặt, hãy xem trang web [Android Studio](https://developer.android.com/studio/index.html#top) để được hướng dẫn về cách tải xuống mọi thứ bạn cần để bắt đầu và chạy.
Nếu bạn chưa từng sử dụng Android Studio, hãy xem qua [First App Tutorial](https://developer.android.com/training/basics/firstapp/index.html) dành cho Android Studio trước khi bắt đầu ứng dụng này.


## Tạo dự án mới

Trong bước này, bạn tạo một dự án hoàn toàn mới trong Android Studio để sử dụng cho ví dụ của chúng tôi. Nếu bạn chưa chạy Studio, hãy tiếp tục và mở nó ngay bây giờ.

#### Bắt đầu hướng dẫn dự án mới

![enter image description here](https://developers.google.com/mobile-ads-sdk/images/android-quickstart-00.png)

Nếu bạn thấy màn hình chào mừng ở trên, hãy chọn **Start a new Android Studio project**. Nếu không, chọn **File**> **New Project** từ trình đơn. Điều này sẽ trả về trình hướng dẫn dự án mới:


#### Tên dự án của bạn

![enter image description here](https://developers.google.com/mobile-ads-sdk/images/android-quickstart-01.png)

Nhập "BannerExample" làm tên ứng dụng và bất kỳ tên miền công ty bạn sử dụng cho ứng dụng của bạn. Android Studio tự động xác định tốt vị trí dự án, nhưng bạn có thể thay đổi nó nếu bạn muốn.

#### Đặt phiên bản SDK bắt buộc
![enter image description here](https://developers.google.com/mobile-ads-sdk/images/android-quickstart-02.png)

Trên màn hình tiếp theo, hãy chọn **Phone and Tablet** cho yếu tố hình thức và phiên bản SDK tối thiểu là 9. Đây là phiên bản tối thiểu được Google Mobile Ads SDK hỗ trợ.

#### Thêm hoạt động chính của bạn
![enter image description here](https://developers.google.com/mobile-ads-sdk/images/android-quickstart-03.png)

Để cho ví dụ đơn giản, vì vậy trên màn hình này chọn **Empty Activity**.

#### Đặt tên hoạt động của bạn
![enter image description here](https://developers.google.com/mobile-ads-sdk/images/android-quickstart-04.png)

Trên màn hình này bạn có tùy chọn chọn tên cho hoạt động của ứng dụng và các tài nguyên có liên quan của nó. Sử dụng các tên mặc định cho ví dụ này, và chỉ cần nhấp vào nút **Finish**.

#### Biên dịch dự án mới của bạn
Sau khi nhấp vào **Finish**, bạn có một dự án làm việc với một hoạt động duy nhất. Hãy thử biên dịch và chạy nó (chọn **Run 'app'** từ trình đơn **Run**). Bạn sẽ thấy một "Hello world!" Tin nhắn trên một màn hình màu xám rỗng. Đừng lo lắng, bạn sẽ thêm một số nội dung khác vào các bước tiếp theo.

## Cấu hình gradle


Gradle là một hệ thống tạo mã nguồn mở và miễn phí, kết hợp một số tính năng tiện dụng cho các nhà phát triển Android (chẳng hạn như quản lý phụ thuộc, như bạn nhìn). Nếu bạn chưa sử dụng nó trước đây, hãy truy cập gradle.org để biết thêm thông tin về cách hoạt động của gradle.

Ở bước này, bạn sẽ sửa đổi tệp **build.gradle**.  Dự án mới của bạn có hai trong số này. Một là tệp cấp dự án trong thư mục gốc **BannerExample**, có các cài đặt ảnh hưởng đến dự án nói chung. Loại khác là cấp ứng dụng có cài đặt cho ứng dụng duy nhất của dự án của bạn. Nó được lưu trong thư mục **BannerExample / app**. Các dự án khác có chứa nhiều ứng dụng sẽ có tệp tin **build.gradle** cấp ứng dụng riêng biệt cho mỗi ứng dụng.

Để sử dụng Mobile Ads SDK trong dự án của bạn, trước tiên bạn cần tham chiếu nó dưới dạng phụ thuộc vào tệp tin `build.gradle` của ứng dụng. Mở `BannerExample / app /build.gradle` và tìm `dependencies` gần phía dưới cùng.

build.gradle (excerpt)

    ...
    dependencies {
            compile fileTree(dir: 'libs', include: ['*.jar'])
            compile 'com.android.support:appcompat-v7:22.2.0'
            compile 'com.google.android.gms:play-services-ads:10.2.0'
        }
    ...

Thêm một đường thẳng vào nó như hình chữ đậm ở trên. Điều này cho phép gradle bao gồm mã từ hiện vật `play-services-ads` , được tìm thấy trong `Google Repository`.

Bạn có thể nhìn thấy thông báo cảnh báo trên đầu cửa sổ Android Studio cho biết rằng phân lớp cần phải thực hiện đồng bộ hóa. Nếu đúng như vậy, hãy nhấp vào **Sync Now** . Gradle sẽ làm mới các thư viện dự án của bạn để bao gồm các phụ thuộc bạn vừa thêm vào.
Nếu đây là lần đầu tiên bạn sử dụng Google Repository, bạn cũng có thể thấy thông báo yêu cầu cài đặt. Nếu điều đó xảy ra, chỉ đồng ý cài đặt và Android Studio sẽ tải xuống cho bạn.
Khi tệp `build.gradle` của bạn được sửa đổi và mọi thứ đã được đồng bộ hóa, hãy thử xây dựng lại dự án (Chạy ứng dụng 'trong trình đơn Chạy) để đảm bảo rằng nó đã được biên dịch chính xác. Bạn sẽ không thấy bất kỳ thay đổi nào, nhưng bao gồm các dịch vụ của Google Play là bước đầu tiên hướng nhận quảng cáo vào ứng dụng của bạn.

## Cung cấp cho ứng dụng của bạn một ID đơn vị quảng cáo


[AD Unit ID](https://support.google.com/dfp_premium/answer/177203) là một số nhận dạng duy nhất được cung cấp cho các địa điểm trong ứng dụng nơi quảng cáo được hiển thị. Ví dụ: nếu bạn có một ứng dụng với hai hoạt động, mỗi banner quảng cáo hiển thị, bạn cần hai đơn vị quảng cáo, mỗi bộ đều có ID riêng.
Để ứng dụng mới của bạn hiển thị quảng cáo, ứng dụng đó cần gồm Ad Unit ID. Mở tệp tài nguyên ứng dụng của bạn, tệp này được tìm thấy tại `BannerExample/app/src/main/res/values/strings.xml`

strings.xml

    <?xml version="1.0" encoding="utf-8"?>
    <resources>
        <string name="app_name">My Application</string>
        <string name="hello_world">Hello world!</string>
        <string name="action_settings">Settings</string>
        <string name="banner_ad_unit_id">/6499/example/banner</string>
    </resources>
Thêm thẻ <string> mới với mã xác nhận duy nhất cho đơn vị quảng cáo. Ad Unit ID được hiển thị ở trên  `/6499/example/banner`, là Google-provided Ad Unit ID của  banner mẫu bạn có thể dùng để thử nghiệm. Bạn nên luôn luôn sử dụng Ads khi phát triển và kiểm thử cho ứng dụng của bạn. Kiểm tra với sản phẩm trực tiếp có thể khiến bạn vi phạm bản quyền DoubleClick For Publishers và có thể dẫn đến tài khoản của bạn bị khóa. Xem tài liệu [addTestDevice](https://developers.google.com/android/reference/com/google/android/gms/ads/AdRequest.Builder#addTestDevice%28java.lang.String%29) để biết thêm thông tim làm thế nào để thử nghiệm Ads với Ad Unit IDs

Mặc dù đây không phải là yêu cầu, nhưng hãy lưu trữ Ad Unit ID trong tệp  resource. Khi ứng dụng của bạn phát triển và đã đến lúc bạn cần quảng cáo, bạn sẽ muốn thay đổi các giá trị ID. Nếu bạn đảm bảo rằng, chúng luôn ở trong tệp resource, bạn sẽ không bao giờ phải tìm kiếm thông qua code của bạn tìm kiếm chúng

## Đặt PublisherAdView vào trong bố cục hoạt động chính của bạn


Tệp Layout chứa định nghĩa XML cho thiết kế trực quan của các sự kiện như hoạt động, các mẩu tin và các mục trong danh sách. Trong bước này, bạn sẽ sửa đổi tệp bố cục cho hoạt động chính **PublisherAdView** ở cuối. Bạn có thể thêm các sự việc vào hoạt động một cách ngẫu nhiên thông qua mã Java, nhưng các tệp  layout cho phép trình bày và hành vi tốt hơn.
Chỉ còn lại hai bước để ứng dụng của bạn sãn sàng hiển thị quảng cáo. Trước tiên, bạn cần sửa đổi layout hoạt động chính gồm `PublisherAdView`. Mở `BannerExample/app/src/main/res/layout/activity_main.xml`trong trình soạn thảo.

activity_main.xml

    <RelativeLayout xmlns:android="http://schemas.android.com/apk/res/android"
        xmlns:tools="http://schemas.android.com/tools" android:layout_width="match_parent"
        xmlns:ads="http://schemas.android.com/apk/res-auto"
        android:layout_height="match_parent" android:paddingLeft="@dimen/activity_horizontal_margin"
        android:paddingRight="@dimen/activity_horizontal_margin"
        android:paddingTop="@dimen/activity_vertical_margin"
        android:paddingBottom="@dimen/activity_vertical_margin"
        tools:context=".MainActivity">
    
        <TextView android:text="@string/hello_world" android:layout_width="wrap_content"
            android:layout_height="wrap_content" />
    
        <com.google.android.gms.ads.doubleclick.PublisherAdView
            android:id="@+id/publisherAdView"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:layout_centerHorizontal="true"
            android:layout_alignParentBottom="true"
            ads:adSize="BANNER"
            ads:adUnitId="@string/banner_ad_unit_id">
        </com.google.android.gms.ads.doubleclick.PublisherAdView>
    
    </RelativeLayout>
Thêm XML:
Tên miền không gian được sử dụng cho Ads

    http://schemas.android.com/apk/res-auto
   Một yếu tố mới cho PublisherAdView của bạn
   Bạn sẽ được yêu cầu cung cấp `layout_width` và `layout_height`. Bạn có thể đặt cả hai để `wrap_content`. Trong thẻ `PublisherAdView` cài đặt `adSize` cho `BANNER` và `adUnitId` cho `@string/banner_ad_unit_id`
   Nếu bạn nhìn thấytham số cuối cùng của thẻ **PublisherAdView**, bạn có thể nhìn thấy nó được gọi như là **adUnitId**. Đây là Ad Unit ID mà PublisherAdView dùng để quảng cáo. Trong trường hợp này, chúng tôi tham chiếu nó đến chuỗi tài nguyên của bạn ở bước cuối, vì vậy **PublisherAdView** sử dụng giá trị đó.
   
## Tải quảng cáo trong lớp MainActivity

Thứ cần thiết trong lần thay đổi cuối cùng này lầ để bạn thêm vào lớp hoạt động chính của ứng dụng một số mã Java nạp một quảng cáo vào `PublisherAdView`.

Mở file `MainActivity.java` của bạn. Nó trên thư mục `BannerExample/app/src/main/java/`, mặc dù đường dẫn thư mục chính xác thay đổi dựa trên tên miền bạn đã sử dụng khi tạo dự án. Khi nó đã được mở trong trình soạn thảo, hãy tìm phương thức `onCreate` trong lớp `MainActivity`:

MainActivity.java (excerpt)

    package ...
    
    import ...
    import ...
    import com.google.android.gms.ads.doubleclick.PublisherAdRequest;
    import com.google.android.gms.ads.doubleclick.PublisherAdView;
    
    public class MainActivity extends ActionBarActivity {
        ...
        protected void onCreate(Bundle savedInstanceState) {
            super.onCreate(savedInstanceState);
            setContentView(R.layout.activity_main);
    
            PublisherAdView mPublisherAdView = (PublisherAdView) findViewById(R.id.publisherAdView);
            PublisherAdRequest adRequest = new PublisherAdRequest.Builder().build();
            mPublisherAdView.loadAd(adRequest);
        }
        ...
    }
#### Thực hiện hai thay đổi này:

 1. Nhập lớp `PublisherAdRequest` và `PublisherAdView`
 2. Thêm code để tìm  `PublisherAdView` trong layout, tạo `PublisherAdRequest`, sau đó tải một quảng cáo vào `PublisherAdView`
 Không sử dụng dòng PublisherAdRequest được hiển thị ở trên nếu bạn đang thử nghiệm. Tham khảo trang  Targeting page để tìm hiểu thêm về cách sử dụng thiết bị kiểm tra và thiết bị IDs.
 Sau khi hoàn thành, bạn đã hoàn tất. Bây giờ, bạn đã có một `PublisherAdView` đầy đủ chức năng trong hoạt động chính của ứng dụng.
 
## Tận hưởng quảng cáo mới được thêm

Ứng dụng của bạn hiện đã sẵn sàng để hiển thị Google Mobile Ads SDK. Chạy lại và bạn sẽ thấy một thanh công cụ kiểm tra được hiển thị ở dưới cùng của màn hình thiết bị:

![enter image description here](https://developers.google.com/mobile-ads-sdk/images/dfp-android-quickstart-09.png)

Bạn đã tích hợp thành công banner quảng cáo vào ứng dụng.



----------


