<html>
 <head>
 <style>
  @font-face{
    font-family: 'myFont';
    src: url('BNazanin.ttf');
  }
  body{
  direction: rtl;
  }
  </style>
 </head>
 <body>
  <p style="direction: rtl;">
ارث بری در برنامه نویسی زمانی استفاده می شود که یک شی یا کلاس مبنی و متکی بر شی یا کلاس دیگری تعریف شود. در js کتابخانه های زیادی برای استفاده راحت تر و بهتر از ارث بری نوشته شده اند که از نوشتار متفاوتی برای پیاده سازی ارث بری استفاده می کنند ولی از آن جایی که در js پیاده سازی شی گرایی به وسیله زنجیره ای از prototype هاست درخود کتابخانه به وسیله prototype پیاده سازی شده است . پیاده سازی  دراین جا به یکی از این روش ها می پردازیم:  
  </p>
  <ul>
  <li>
  <p>
در js فقط شی داریم و در این¬جا منظور از کلاس شی است که کاربردی مشابه کلاس در زبان¬های برپایه کلاس دارد. هر کلاسی برای ساخته شدن باید از کلاس موجود دیگری ارث برد و تمام کلاس ها از یک کلاس واحد به نام Class ارث می برند ( به صورت مستقیم یا به وسیله تعدادی رابطه پدر-فرزندی) در نتیجه اگرمی خواستیم کلاسی تعریف کنیم که بچه کلاس تعریف شده ای نیست باید از Class ارث ببرد. تعریف ارث بری به طریق زیر است :
  </p>
  <p style="direction: ltr;">
  Var Child = Parent.extend(prop);
  </p>
  <p>
  که prop یک دیکشنری است که کلیدهای آن اسم توابع و مقادیر آن خود توابع هستند.
  </p>
  </li>
  <li>
  <p>
در کلاس فرزند نیاز به دسترسی به متد هایی از کلاس پدر داریم که در کلاس فرزند تغییراتی در آن ها بوجود آورده ایم (آن ها را override کرده ایم). در این صورت متد ._super() در داخل متد تغییر داده شده شده فرزند قابل استفاده است و همان متد از پدر را صدا می زند.
  </p>
  </li>
  </ul>
  <p>
در ادامه مثالی برای نحوه پیاده سازی ارث بری به این روش می آوریم :
</p>
 <p  style="direction: ltr;">
  var Person = Class.extend({<br>
  init: function(isDancing){<br>
    this.dancing = isDancing;<br>
  },<br>
  dance: function(){<br>
    return this.dancing;<br>
  }<br>
});<br>
 <br>
var Ninja = Person.extend({<br>
  init: function(){<br>
    this._super( false );<br>
  },<br>
  dance: function(){<br>
    // Call the inherited version of dance()<br>
    return this._super();<br>
  },<br>
  swingSword: function(){<br>
    return true;<br>
  }<br>
});<br>
 <br>
var p = new Person(true);<br>
p.dance(); // => true<br>
  <br>
var n = new Ninja();<br>
n.dance(); // => false<br>
n.swingSword(); // => true<br>
 <br>
// Should all be true<br>
p instanceof Person && p instanceof Class &&<br>
n instanceof Ninja && n instanceof Person && n instanceof Class<br>
  </p>
  <p>
  در این روش کلاس ما در ظاهربه صورت یک دیکشنری است که به عنوان ورودی در)  Parent.extend( می آید ولی درعمل اتفاقی که می افتد این است که برای ساختن کلاس جدید ابتدا از کلاس پدر یک  instanceجدید می سازیم و به ترتیب برای توابع آن چک می شود که اگر کلاس پدر نیز آن را دارد تغییرات لازم اعمال شود ( در این جا از متد apply بهره می بریم) و درغیر این صورت به کلاس اضافه شوند.
<br>
هم چنین نیازی به ایجاد یک Instance جدید کامل از کلاس پدر همراه با صدا کردن constructor آن وجود ندارد (صدا کردن constrctor می تواند هزینه زیادی داشته باشد) و تنها می خواهیم از فواید استفاده از ‘instanceof’ بهره ببریم برای همین از متغیر initializing استفاده می کنیم که در زمان instanciation یک کلاس اگر مقدار1 داشته باشد constructor آن صدا زده نمی شود.  
  </p>
 </body>
