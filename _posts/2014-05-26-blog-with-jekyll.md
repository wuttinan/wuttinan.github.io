จดโดเมนชื่อตัวเองไว้ ตอนแรกจะใช้แค่ทดสอบโปรแกรมส่วนตัวเพื่อประกอบการทำวิทยานิพนธ์ใน aws เฉยๆ พอเลิกใช้แล้วก็เสียดายโดเมน ก็เลยว่าจะทำบล็อกเขียนโน่นนี่ไปเรื่อย จะเช่าโฮสท์เลยก็กะไรอยู่ สิ้นเปลือง เพราะนานๆ เขียนที หลังจากค้นๆ ดูไปเรื่อย เห็นว่าใน github มีพื้นที่ให้ใช้ฟรีทาง [github pages](https://pages.github.com) แถมเชื่อมกับโดเมนของตัวเองได้ด้วย (แต่ถ้าไม่อยากจดก็ใช้ `username.github.io`) เลยเข้าทาง

โดยเจ้า github pages นี่พ่วง [jekyll](http://jekyllrb.com) มาให้ด้วย ซึ่งเป็น static site generator ตัวนึง ซึ่งเหมาะสมกับการเขียนบล็อกดี ไม่ต้องวุ่นเรื่อง database นั่นโน่นนี่ จุบจิบ เหมือนพวก wordpress, drupal อะไรพวกนี้ แถมไฟล์เล็กกว่าด้วย ไม่เปลืองทีเปลืองทาง

หลังจากค้นๆ ดูไปอีก ก็เจอ repo ตัวนึง ชื่อว่า [poole](http://getpoole.com) หน้าตาถูกใจ ขาวสะอาดดี มีธีมย่อยให้ใช้อีกสองอันตามความชอบ ยังทำให้การติดตั้งบล็อกบน github pages ของเราง่ายขึ้นไปอีก แค่เปิด repo ของตัวเองขึ้นมาหนึ่งอัน ดาวน์โหลดไฟล์ทั้งหมดใน [repo ของ poole](https://github.com/poole/poole/) แก้ไฟล์ config ให้เหมาะกับของตัวเองนิดหน่อย แล้วใส่กลับเข้าไปใน repo ของเรา เรียบร้อยโรงเรียนจีน รวมทั้งหมดก็ไม่เกินสิบนาทีได้ ได้บล็อกแล้ว

## first time

ตอนแรกเราจะได้ไฟล์และโฟลเดอร์หน้าตาแบบนี้ใน repo ของเรา

```
/_includes
/_layouts
/_posts
/public
_config.yml
404.html
LICENSE.md
README.md
about.md
atom.xml
index.html

```

หลักๆ ที่น่าสนใจก็มี

* `/_includes` กับ `/_layouts` นี่เก็บไฟล์ html ของหน้าบล็อก ใครจะแก้หน้าตายังไงมาแก้ตรงนี้
* `/_posts` คือที่ที่เก็บโพสท์ของเรา เวลาสร้างไฟล์โพสท์อะไรก็มาแปะตรงนี้
* `_config.yml` นี่คือไฟล์ตั้งค่า เข้ามาแก้ชื่อ แก้ url อะไรที่ตรงนี้

---

## posting

การเขียนบล็อก สร้างไฟล์ขึ้นมาหนึ่งไฟล์ โดยตรงหัวต้องมีค่าต่างๆ แบบง่ายสุดเลยก็คือ

```
---
layout: post
title: example
---

your post content
```

* `layout:` นี่เป็นตัวบอกว่าหน้าที่เราจะเขียนนี้เป็นแบบไหน
* `title:` ก็คือหัวเรื่องของสิ่งที่เราจะเขียน
* ตัวเนื้อหาที่จะเขียนให้เขียนด้วย [markdown](http://daringfireball.net/projects/markdown/)
* จริงๆ มีอีกนะ ลองเข้าไปดูเพิ่มใน [front-matter](http://jekyllrb.com/docs/frontmatter/)

เมื่อต้องการจะเผยแพร่แล้ว ตั้งชื่อไฟล์เป็น `YYYY-MM-DD-title.md` แล้วโยนไฟล์เข้าไปใน `/_posts`

---

## customization
พอลองดูแล้วรู้สึกมันยังขาดอะไรไปหน่อย ก็เลยปรับให้เข้ารูปเข้ารอยตามที่ต้องการ เรียงๆ ตามนี้ ปรับแต่งได้ตามใจตนเองเลย ส่วนตัวอยากได้ประมาณนี้

### 1. static page

ถ้าอยากทำ static page เช่น หน้า about หรืออะไรก็ตามแต่ สร้างไฟล์เหมือนโพสท์ปกติ แต่เปลี่ยนค่า `layout:` ให้เป็น `page` ตรงหัวไฟล์แค่นั้น แล้วจับโยนเข้าโฟลเดอร์บนสุด

```
---
layout: page
title: example page
---

your page content
```

เวลาเข้าหน้านี้ก็แค่ `yoursite.name/pagename`

### 2. archive page

ตัวบล็อกไม่มีหน้ารวมโพสท์ไว้ จึงต้องสร้างไฟล์ `archive.md` ขึ้นมาอีกไฟล์นึง ข้างในเป็นหน้าตาอย่างนี้
{% highlight html %}
{% raw %}
---
layout: page
title: Archive
---

## Blog Posts

{% for post in site.posts %}
  * {{ post.date | date_to_string }} &raquo; [ {{ post.title }} ]({{ post.url }})
{% endfor %}
{% endraw %}
{% endhighlight %}
เสร็จแล้วก็จับโยนใส่บนโฟลเดอร์บนสุดเลย เวลาเข้าก็เข้าทาง `yoursite.name/archive`


### 3. site navigation

header ของบล็อกที่ให้มาตอนแรกมีแค่ชื่อกับคำโปรย ส่วนตัวอยากแทนที่ตรงคำโปรยนั้นด้วยลิงค์สามอัน คือหน้าประวัติส่วนตัว หน้ารวมโพสท์ และลิงค์ไปยังไฟล์ `atom.xml` เผื่อใครเอาไปดูผ่านพวก feed reader ทั้งหลาย

อันดับแรกเลย เพิ่มโค้ดนี้เข้าไปในไฟล์ `_config.yml`

```
pages_list:
  About: '/about'
  Archive: '/archive'
  Feed: '/atom.xml'

```

ใครอยากเพิ่มลิงค์อะไรก็แก้เข้าไปเพิ่มนอกจากนี้ได้เลย

ลำดับต่อมาก็ไปแก้ไฟล์ `/_layouts/default.html` ให้เป็นแบบนี้
{% highlight html %}
{% raw %}
<h3 class="masthead-title">
<a href="/" title="Home">{{ site.title }}</a>

{% for page in site.pages_list %}
  &nbsp;&nbsp;&nbsp;
  <small><a href="{{ page[1]  }}">{{ page[0] }}</a></small>
{% endfor %}
</h3>
{% endraw %}
{% endhighlight %}

### 4. others

* สำหรับคนที่อยากใส่ระบบ comment และ google analytics ลองดูต่อ[ที่นี่](http://joshualande.com/jekyll-github-pages-poole/) เขาเขียนไว้ค่อนข้างครบมาก
* [redirects on github pages](https://help.github.com/articles/redirects-on-github-pages)
* [jemoji](https://help.github.com/articles/emoji-on-github-pages)

---

## custom domain name

ใครที่จดโดเมนเอง ทาง github เขาก็[ให้ใช้ได้](https://help.github.com/articles/setting-up-a-custom-domain-with-github-pages)ด้วยนะ ให้สร้างไฟล์ `CNAME` ขึ้นมาอันนึง ข้างในเป็นชื่อโดเมนของเราเอง จับโยนใส่โฟลเดอร์บนสุด

```
yoursite.name
```
เสร็จแล้วก็ไปแก้โดเมนตัวเองให้ชี้มาที่นี่ โดยใช้ ip นี้ `192.30.252.153` กับ `192.30.252.154` ก็เป็นอันเรียบร้อย

---

## least but not last

เท่านี้ก็น่าจะได้บล็อกแบบเรียบง่ายขึ้นมาอันนึงแล้ว เจออะไรใหม่ๆ จะพยายามเข้ามาอัพเดทเรื่อย ถ้าจะคอมเมนท์หรือมีคำถามอะไร ถามได้ที่ [twitter](http://twitter.com/wuttinan) เลยฮะ :D
