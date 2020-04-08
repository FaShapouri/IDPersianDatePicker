
<div dir='rtl'>

  # 🗓 🇮🇷 انتخاب‌گر تاریخ پارسی
  
  خود آی‌او‌اس یه DatePicker داره که میشه Locale و Calendar رو براش به بطوری تنظیم کرد تا باهاش بتونیم یه تاریخ پارسی انتخاب کنیم. اما شخصا بنظرم زیاد جالب نبود؛ چون با استفاده از اون:

  - هربار فقط میشه <b>یک</b> تاریخ رو انتخاب کرد.
  - از فونت پیشفرض خود سیستم عامل استفاده می‌کنه.
  - خوشگل نیست.

  برای همین تصمیم گرفتم یه چیزی پیاده‌سازی کنم تا این ویژگی‌ها/ایرادات رو نداشته باشه. چندتا عکس هم ازش قرار دادم، تا بتونین یه نگاهی (قبل از استفاده) بهش بندازین.

  <table>
    <tr>
      <td><img src='./Images/0.png'></td>
      <td><img src='./Images/1.png'></td>
      <td><img src='./Images/2.png'></td>
    </tr>
  </table>

  <h1>نصب</h1>
  <p>
  برای نصب می‌تونین از <code>Cocoapod</code> استفاده کنین. عبارت مورد استفاده برای نصب هم اینه:

  <pre dir='ltr'>pod 'IDPersianDatePicker'</pre>

  </p>

  <p>👈 توجه داشته باشین که زبان مورد استفاده توی این پروژه <span style='font-weight: bold; color: orange;'>سوییفت نسخه ۴.۲</span> بوده. </p>

  <h1>استفاده</h1>

  <h2>قدم اول</h2>
  <p>اولین قدم اینه که ایمپورتش کنین: </p>
  <div dir='ltr'>
  
```swift
import PersianDatePicker
```

  </div>

  👈 توجه داشته باشین که برای نصب از <code>IDPersianDatePicker</code> استفاده شد، ولی برای ایمپورت از <code>PersianDatePicker</code> استفاده شد. دلیل این مورد این هست که کتابخانه دیگه‌ای با نام <code>PersianDatePicker</code> توی پادها موجود بود، و برای همین مجبور شدم این ابزار رو با نام دیگه‌ای توی Cocoapod منتشر کنم.

  <h2>قدم دوم</h2>
  <p>مرحله بعد اینه که ویوکنترلر شما یه پروتکل رو پیاده‌سازی کنه. پروتکلی که باید پیاده‌سازی کنه <code>PersianDatePickerDelegate</code> هست. وظیفه این پروتکل آماده کردن داده‌ها و مشخصه‌های مورد استفاده در انتخاب‌گر هست.<br>
  متدها و مشخصه‌هایی که داره بصورت زیر هست:

  <ul>
    <li>متد <code dir='ltr'>persianDatePicker(canSelectDate date: Date)</code> و خروجی از نوع <code dir='ltr' style='color: #3498DB;'>Bool</code>
    <p>با استفاده از این متد می‌تونین از انتخاب یه سری روزها جلوگیری کنین.</p><br>
    </li>
    <li>متد <code dir='ltr'>persianDatePicker(didSelectDates dates: [Date])</code>
    <p>زمانیکه که کاربر روی دکمه انتخاب بزنه، روزهایی که انتخاب شده، با استفاده از این متد در دسترس خواهند بود.</p><br>
    </li>
  </ul>
  </p>

  ## قدم سوم

  برای فراخوانی و نمایش انتخاب‌گر هم بصورت زیر عمل می‌کنیم:

  <div dir='ltr'>

```swift
PersianDatePicker.Present(
  sourceController : UIViewController,
  configuration    : PersianDatePicker.Configuration,
  delegate         : PersianDatePickerDelegate,
  completion       : (() -> Void)?
)
```

  </div>

  ### تنظیمات (یا همون <code>PersianDatePicker.Configuration</code>)

  توی این نسخه، تنظیمات مورد نیاز انتخاب‌گر رو از <code>delegate</code> جدا کردم. الان موقع نمایش باید تنظیمات مورد نیاز رو بسازین و ارجاع بدین. این تنظیمات به چند بخش اصلی تقسیم می‌شن:

  #### تنظیمات رابط کاربری (**مشخصه <code>ui</code>**)

  <div dir='ltr'>

  ```swift
  var font: UIFont = .systemFont(ofSize: 16, weight: .regular)
  ```

  </div>

  - فونت مورد استفاده رو مشخص می‌کنه.

  <br>

  <div dir='ltr'>

  ```swift
  var selectedDayTextColor: UIColor	= .black
  ```

  </div>

  - رنگ مورد استفاده برای متن المان‌های انتخاب‌شده رو مشخص می‌کنه.

  <br>

  <div dir='ltr'>

  ```swift
  var selectedDayBackgroundColor: UIColor = /* a_beautiful_color */
  ```

  </div>

  - رنگ مورد استفاده برای پس‌زمینه المان‌های انتخاب‌شده رو مشخص می‌کنه.

  <br>

  
  #### تنظیمات متن‌ها (**مشخصه <code>texts</code>**)

  <div dir='ltr'>

  ```swift
  var title: String = "تاریخ مورد نظر خود را انتخاب نمایید"
  ```

  </div>

  - عنوان مورد نظر برای نمایش.

  <br>

  <div dir='ltr'>

  ```swift
  var message: String? = nil
  ```

  </div>

  - توضیح مورد نظر برای نمایش.

  <br>

  #### تنظیمات انتخاب تاریخ(ها) (**مشخصه <code>selection</code>**)

  <div dir='ltr'>

  ```swift
  var minimumDate: Date
  var maximumDate: Date
  ```

  </div>

  - اینها تاریخ کمینه و بیشینه رو توی تقویم مشخص می‌کنن.

  <br>

  <div dir='ltr'>

  ```swift
  var canSelectMultipleDates: Bool = false
  ```

  </div>

  - این مشخصه بیانگر اینه که آیا میشه چندین تاریخ رو انتخاب کرد، یا فقط مجاز به انتخاب یک تاریخ هست.
  - مقدار پیش‌فرض این مشخصه برابر <code>false</code> هست.

  <br>

  <div dir='ltr'>

  ```swift
  var preselectedDates: [Date] = []
  ```

  </div>

  - این مشخصه، تاریخ‌هایی رو مشخص می‌کنه که بصورت پیش‌فرض انتخاب‌شده هستن.
  - اگه این مشخصه خالی نباشه، بصورت پیش‌فرض صفحه‌ای به کاربر نمایش داده میشه، که کوچک‌ترین تاریخ انتخاب‌شده داخل‌اش باشه. 

  <br>

  <div dir='ltr'>

  ```swift
  var defaultDay: Date? = nil
  ```

  </div>

  - این مشخصه، تاریخ پیش‌فرض تقویم برای نمایش هست. یعنی اگر این مشخصه مقدار داشته باشه، صفحه‌ای از تقویم بطور پیش‌فرض نمایش داده میشه که این تاریخ داخل‌اش باشه.
  - مقدار پیش‌فرض این مشخصه برابر <code>nil</code> هست.
  - زمانیکه تاریخ از پیش تعیین‌شده‌ای نداشته باشیم، و این مشخصه هم مقدار نداشته باشه، بصورت پیش‌فرض صفحه اول مجاز تقویم به کاربر نمایش داده میشه؛ یعنی صفحه‌ای که <code>minimumDate</code> داخل‌اش هست.
  - برای تنظیم صفحه پیش‌فرض تقویم، **بررسی این مشخصه اولویت بالاتری نسبت به <code>preselectedDates</code> دارد**.

  <br>


  ## سخن آخر

  - 👀 اگه ایرادی توی روند پیاده‌سازی یا استفاده مشاهده کردین، حتما بگین تا رفعش کنیم. 
  - 🤝 اگه قابلیت خاصی به ذهن‌تون رسید که می‌تونست به بهتر شدن این پروژه کمک کنه، حتمن بگین؛ شاید با کمک هدیگه پیاده‌سازی‌اش کردیم.
  - 😋 تنکیوووووو. 
  
  
</div>
