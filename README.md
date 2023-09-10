# HTML-CSS-from-scratch-to-pro

# How to Responsive

## css units

1. absolute units

- px (fig unit)

2. relative units

- relative to font-size
  - em
  - rem
- relative to the viewport
  - vw
  - vh
  - vmin
  - vmax

3. percentage

- ส่วนใหญ่ใช้กับ width
- มันจะ relative กับ parent
- block element width default 100%

## Controlling the width of images

- `<img />` เป็น inline element
- inline element จะมี width ตามขนาด content
- img เวลากำหนด width หรือ height ถ้ากำหนด อย่างใดอย่างหนึ่ง มันจะ auto อีกอันให้
  - กำหนด widht อย่างเดียว => จะ auto height ให้
  - กำหนด height อย่างเดียว => จะ auto widht ให้
- การกำหนด max-width ให้ img มันเป็นการ set เพื่อให้ width ของ img ไม่ใหญ่เกิน original size (เพราะถ้ามันเกิน original size มันจะเสียคุณภาพของ img)

## min-width and max-width

- เราสามารถ set max-width ที่เราต้องการ โดยที่เรายัง keep percentage(width percentage) ที่เรากำหนด (สำหรับ container)
  - ทำให้ตอนกางมันจะไม่กางเกิน max-width
  - แล้วตอนหุบมันก็จะหุบ responsive ให้ได้เรื่อยๆ เพราะไม่มีการ set min-width
- เราไม่ควร set min-width ให้ container เพราะเราควรให้มันหุบแล้วขนาดปรับ auto โดยที่ไม่มีการกำหนด minimum-width ให้มัน
- max-width,min-width จะ depend on layout ที่มันถูก set

## Relative unit

### relative to font-size

1. em

- relative กับ parent ของมัน
- font-size เป็น property ที่ inherit ได้
  - ปกติถ้าเราไม่กำหนด default มันจะเป็น 16px (inherit จาก body)
  - ถ้าเราไม่กำหนด font-size เลย font-size default จาก body มันจะ inherit มาให้ auto
- `em มีข้อเสียตรง` ที่มัน relative กับ parent แล้วถ้าเรามี nested element แล้วเรามีการกำหนด em ให้มันมันจะทำให้เกิด massive font-size ที่เราไม่ต้องการ เพราะมันเกิดการคูณขนาดซ้อนทับมาเรื่อยๆ จากคุณสมบัติของ em (relative กับ parent สืบทอดกันมาเรื่อยๆ ยิ่ง level element ลึกเท่าไร ยิ่ง massive มากเท่านั้น) [`cascading effect`]
- em ถ้าใช้กับ font-size มันจะ relative กับ parent แต่ถ้าใช้กับ property อื่นมันจะไม่ได้ relative กับ parent แล้ว แต่จะ relative กับ font-size ของ element แทน

2. rem

- relative กับ root element (html element)

## How to decide which unit to use

- font-size => ใช้ rem เพื่อป้องกัน `cascading effect`
- padding,margin => ใช้ em (ถ้าไม่ใช่ property font-size em มันจะ relative กับ font-size ของ element ทำให้ padding,margin จะปรับตามขนาด font-size ของ element แทน)
- width => em,percentage,px

`Note :` เป็นกฎอย่างง่ายๆ

## Block and inline

1. block element => width กางเต็ม 100% เรียงจากบนลงล่าง stack ลงมาเรื่อยๆ

- div,header,footer,main, etc.
- h1->h6
- p

2. inline element => width จะกางตาม content เรียงจากซ้ายไปขวาต่อกันไปเรื่อยๆ

- a
- strong
- em
- span

## Flexbox

- ตอนกำหนด display flex
  - เรากำหนด width ให้แต่ละ flex item ด้วย % (แบ่งตามสัดส่วนที่เราต้องการ)

### spacing ของ flex item

- เราสามารถใช้ margin ได้ในการ set spacing ระหว่าง flex item (แต่ปัญหาคือเราไม่รู้ว่าต้องใช้ margin เท่าไร แล้วก็มันอาจะไม่ fit กับ content)
- ปกติถ้าเราไม่กำหนด justify-content แล้ว flex item width รวมกัน ไม่ได้เต็ม width ของ flex container มันจะเหลือ space
- justify-content: space-between; มันจะเอา space ที่เหลือนี้มาทำ ช่องว่างระหว่าง flex item
- justify-content: space-around; มันจะเอา space ที่เหลือมาคำนวณ ช่องว่างระหว่าง flex item ให้มีพื้นที่ซ้าย-ขวา
- justify-content: space-evenly; มันจะเอา space ที่เหลือมาคำนวณ ช่องว่างระหว่าง flex item ให้เท่าๆกัน
- ถ้า width ของ flex item รวมกันแล้วเต็ม width ของ flex container พอดี มันจะไม่เหลือ space เอามาทำ justify-content
- ซึ่งตอน set width เป็น % อาจจะต้องให้มันรวมกันแล้วไม่เท่ากับ 100% เพื่อให้เหลือ space เอามาใช้ทำ justify-content

### controlling the vertical position of flex items

- ถ้า div(block element) เป็น flex item มันจะ stack จากซ้ายไปขวาแทน stack บนลงล่าง
  - แล้วก็ stretch height ของ div
  - stretch height เท่ากับ flex item ที่สูงที่สุด [flex item ทุกตัวก็จะสูงตาม flex item ที่สูงที่สุด : align-items:stretch (default)]
  - default height ของ div(block element) -> height:0 ซึ่งมันสามารถ grow to fit กับ content ที่อยู่ข้างในมัน
- align-items
  - flex-start (flex item แต่ละตัวจะสูงตาม content ของมัน)
  - center (flex item แต่ละตัวจะสูงตาม content ของมัน)
  - flex-end (flex item แต่ละตัวจะสูงตาม content ของมัน)
  - baseline (flex item แต่ละตัวจะสูงตาม content ของมัน) => ตำแหน่งของ first line of text ของทุกๆ flex item จะเท่ากัน
  - stretch (default) (flex item ทุกตัวก็จะสูงตาม flex item ที่สูงที่สุด)

### flex direction

- flex-direction:row; (default) => เป็นการกำหนด main axis (row,column)
- flex-direction:row; -> main axis จะกลายเป็นแนวนอน row (parent จะกลายเป็น row แล้ว children จะกลายเป็น column)
- flex-direction:column; -> main axis จะกลายเป็นแนวตั้ง column (parent จะกลายเป็น column แล้ว children จะกลายเป็น row)
- justify-content depend on main axis
- align-items depend on cross axis

## Media Query basics

```
@media 'media-type' and ('media-condition') {...}
```

- media type,media condition ต่างก็เป็น optional อาจจะไม่จำเป็นต้องเรียกใช้ทั้ง 2 ตัวก็ได้ เรียกใช้แค่อย่างใดอย่างนึงก็ได้
  - @media screen and (min-width: 960px) {...}
  - @media screen and (orientation: portrait) {...}
  - @media (min-width: 960px) {...} -> from a minimum width of 960px and bigger (ใหญ่กว่า min-width)
  - @media (max-width: 960px) {...} -> from a maximum width of 960px and smaller (เล็กกว่า max-width)
  - @media (min-width: 400px) and (max-width: 960px) {...} -> ใหญ่กว่า min-width 400px และ เล็กกว่า max-width 960px (`400px < range < 960px`)
  - @media (min-width: 400px) and (orientation: landscape) {...}
- ลำดับการวาง media query มีผล
  - @media (min-width: 400px) {...},@media (min-width: 650px) {...} => ทำตามลำดับ min-width 400px,650px
  - @media (min-width: 650px) {...},@media (min-width: 400px) {...} => จะไม่ทำ min-width: 650px เพราะมันโดน min-width: 400px overide (min-width 650px include อยู่ใน min-width 400px)

### media type

- Screen => @media screen {...}
- Print => @media print {...}
- Speech => @media speech {...}

### media condition

- let us target specific conditions within that media type
- widths -> @media (min-width: 600px) {...}
- orientations -> @media (orientation: landscape) {...}
  - orientation: landscape => it's wider than it's tall (กว้างมากกว่าสูง)
  - orientation: portrait => it's taller than it's wider (สูงมากกว่ากว้าง)
- specific features -> @media (hover) {...}
