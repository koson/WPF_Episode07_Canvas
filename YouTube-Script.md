# สคริปต์การสอน: WPF Episode 07 - Canvas

## เนื้อหาที่จะสอน

### 1. Canvas คืออะไร
- Panel สำหรับควบคุมตำแหน่งแบบ Absolute Positioning
- ใช้พิกัด X, Y โดยตรง

### 2. Canvas Properties
- Canvas.Left, Canvas.Top
- Canvas.Right, Canvas.Bottom
- Canvas.ZIndex (Layer)

### 3. การใช้งาน
- วาดรูปทรงต่างๆ
- จัดตำแหน่งแบบแม่นยำ
- สร้าง Drawing/Animation

---

## ส่วนที่ 1: Introduction (0:00 - 2:00)

**สวัสดีครับทุกคน**

ยินดีต้อนรับกลับมาสู่ WPF Tutorial Series ของเรา

วันนี้เราจะมาเรียนรู้เกี่ยวกับ **Canvas** ซึ่งเป็น Layout Panel ที่แตกต่างจากทุก Panel ที่เราเรียนมาครับ

Panel ที่ผ่านมา เช่น StackPanel, Grid, WrapPanel, DockPanel 
ทั้งหมดจะช่วยจัด Layout อัตโนมัติให้เรา

แต่ **Canvas ต่างครับ!** 

Canvas ให้เราควบคุมตำแหน่งเองทุกอย่าง ด้วยพิกัด X, Y แบบ **Absolute Positioning**!

---

## ส่วนที่ 2: Absolute Positioning คืออะไร (2:00 - 5:00)

### Demo 2.1: แนวคิดของ Canvas

**Absolute Positioning** หมายถึงการบอกตำแหน่งที่แน่นอนเป็น pixels

เหมือนการวาดรูปบนกระดาษ:
- กำหนดว่าจุดนี้อยู่ห่างจากซ้าย 100 pixels
- และห่างจากบน 50 pixels

```xml
<Canvas>
    <Ellipse Canvas.Left="100" Canvas.Top="50" 
             Width="80" Height="80" 
             Fill="Red"/>
</Canvas>
```

**อธิบาย:**
- `Canvas.Left="100"` - ห่างจากขอบซ้าย 100 pixels
- `Canvas.Top="50"` - ห่างจากขอบบน 50 pixels
- วงกลมจะอยู่ที่ตำแหน่งนั้นเสมอ ไม่เปลี่ยน

### Demo 2.2: ต่างจาก Panel อื่นอย่างไร

**Panel อื่นๆ (Automatic Layout):**
- StackPanel - เรียงต่อกันอัตโนมัติ
- Grid - แบ่งเป็น Row/Column
- WrapPanel - ขึ้นบรรทัดใหม่เอง
- DockPanel - Dock ไปที่ขอบ

**Canvas (Manual Layout):**
- บอกตำแหน่งเองทุก Element
- ไม่มีการจัดอัตโนมัติ
- ควบคุมได้แม่นยำ 100%

---

## ส่วนที่ 3: Canvas.Left และ Canvas.Top (5:00 - 10:00)

### Demo 3.1: Canvas.Left

```xml
<Canvas Background="LightGray" Height="300">
    <Ellipse Canvas.Left="50" Canvas.Top="100" 
             Width="80" Height="80" 
             Fill="Red"/>
</Canvas>
```

**Canvas.Left** - ระยะห่างจากขอบซ้าย

### Demo 3.2: Canvas.Top

```xml
<Canvas Background="LightGray" Height="300">
    <Ellipse Canvas.Left="100" Canvas.Top="50" 
             Width="80" Height="80" 
             Fill="Blue"/>
</Canvas>
```

**Canvas.Top** - ระยะห่างจากขอบบน

### Demo 3.3: วาดหลายรูป

ตอนนี้เราลองวาดหลายรูปในตำแหน่งต่างๆ กัน

```xml
<Canvas Background="#F5F5F5" Height="400">
    <!-- วงกลมสีแดง -->
    <Ellipse Canvas.Left="50" Canvas.Top="50" 
             Width="80" Height="80" 
             Fill="Red"/>
    
    <!-- สี่เหลี่ยมสีน้ำเงิน -->
    <Rectangle Canvas.Left="200" Canvas.Top="100" 
               Width="100" Height="60" 
               Fill="Blue"/>
    
    <!-- วงกลมสีเขียว -->
    <Ellipse Canvas.Left="350" Canvas.Top="80" 
             Width="60" Height="60" 
             Fill="Green"/>
    
    <!-- สี่เหลี่ยมสีส้ม -->
    <Rectangle Canvas.Left="100" Canvas.Top="200" 
               Width="80" Height="80" 
               Fill="Orange"/>
</Canvas>
```

**เห็นไหมครับ:**
- แต่ละรูปอยู่ที่ตำแหน่งที่เรากำหนด
- ไม่มีการเรียงอัตโนมัติ
- ควบคุมได้ตามต้องการ

---

## ส่วนที่ 4: Canvas.Right และ Canvas.Bottom (10:00 - 13:00)

### Demo 4.1: Canvas.Right

นอกจาก Left/Top แล้ว ยังมี Right/Bottom ด้วย

```xml
<Canvas Background="LightGray" Height="300">
    <Ellipse Canvas.Right="50" Canvas.Top="50" 
             Width="70" Height="70" 
             Fill="Purple"/>
</Canvas>
```

**Canvas.Right** - ระยะห่างจากขอบขวา

### Demo 4.2: Canvas.Bottom

```xml
<Canvas Background="LightGray" Height="300">
    <Ellipse Canvas.Left="50" Canvas.Bottom="50" 
             Width="70" Height="70" 
             Fill="Orange"/>
</Canvas>
```

**Canvas.Bottom** - ระยะห่างจากขอบล่าง

### Demo 4.3: Right + Bottom

สามารถใช้ร่วมกันได้

```xml
<Canvas Background="LightGray" Height="300">
    <Ellipse Canvas.Right="50" Canvas.Bottom="50" 
             Width="70" Height="70" 
             Fill="Purple"/>
</Canvas>
```

วงกลมจะอยู่มุมล่างขวา!

**หมายเหตุ:**
- ถ้าใช้ Left ก็ไม่ต้องใช้ Right
- ถ้าใช้ Top ก็ไม่ต้องใช้ Bottom
- โดยปกติใช้ Left + Top เป็นหลัก

---

## ส่วนที่ 5: Canvas.ZIndex (13:00 - 18:00)

### Demo 5.1: ปัญหา Overlapping

ถ้า Element ทับกัน จะเกิดอะไรขึ้น?

```xml
<Canvas Background="LightGray">
    <Rectangle Canvas.Left="100" Canvas.Top="100" 
               Width="150" Height="100" 
               Fill="Red"/>
    
    <Rectangle Canvas.Left="150" Canvas.Top="130" 
               Width="150" Height="100" 
               Fill="Blue"/>
</Canvas>
```

**Element ที่เขียนทีหลัง จะอยู่บนสุด!**

สี่เหลี่ยมสีน้ำเงินจะทับสีแดง

### Demo 5.2: ใช้ Canvas.ZIndex

แต่เราสามารถควบคุมได้ด้วย **ZIndex**!

```xml
<Canvas Background="LightGray">
    <Rectangle Canvas.Left="100" Canvas.Top="100" 
               Width="150" Height="100" 
               Fill="Red"
               Canvas.ZIndex="10"/>
    
    <Rectangle Canvas.Left="150" Canvas.Top="130" 
               Width="150" Height="100" 
               Fill="Blue"
               Canvas.ZIndex="5"/>
</Canvas>
```

**ตอนนี้ Red จะอยู่บน Blue!**

เพราะ ZIndex ของ Red (10) > Blue (5)

### Demo 5.3: ZIndex คืออะไร

**ZIndex** = "Layer" หรือ "ชั้น"

- ZIndex สูง = อยู่บนสุด (ใกล้ตาเรา)
- ZIndex ต่ำ = อยู่ด้านล่าง
- Default ZIndex = 0

คิดเหมือนกับชั้นของกระดาษ:
- กระดาษชั้นบนสุด = ZIndex 10
- กระดาษชั้นกลาง = ZIndex 5
- กระดาษชั้นล่าง = ZIndex 0

### Demo 5.4: ตัวอย่างจริง - Text บน Shape

```xml
<Canvas Background="#F5F5F5">
    <Ellipse Canvas.Left="100" Canvas.Top="100" 
             Width="200" Height="150" 
             Fill="LightBlue"
             Canvas.ZIndex="1"/>
    
    <TextBlock Canvas.Left="250" Canvas.Top="200" 
               Text="Canvas Demo" 
               FontSize="32" 
               FontWeight="Bold"
               Canvas.ZIndex="10"/>
</Canvas>
```

Text จะอยู่บนวงกลมเสมอ เพราะ ZIndex สูงกว่า!

---

## ส่วนที่ 6: ตัวอย่างการใช้งานจริง (18:00 - 25:00)

### 6.1 Game Scene

Canvas เหมาะมากสำหรับทำ Game!

```xml
<Canvas Width="600" Height="400" Background="SkyBlue">
    <!-- พื้นหญ้า -->
    <Rectangle Canvas.Left="0" Canvas.Bottom="0" 
               Width="600" Height="100" 
               Fill="Green"/>
    
    <!-- ดวงอาทิตย์ -->
    <Ellipse Canvas.Right="50" Canvas.Top="50" 
             Width="80" Height="80" 
             Fill="Yellow"/>
    
    <!-- ตัวละคร -->
    <Rectangle Canvas.Left="100" Canvas.Bottom="100" 
               Width="40" Height="60" 
               Fill="Red"
               Canvas.ZIndex="10"/>
    
    <!-- ต้นไม้ -->
    <Rectangle Canvas.Left="300" Canvas.Bottom="100" 
               Width="20" Height="80" 
               Fill="Brown"/>
    <Ellipse Canvas.Left="280" Canvas.Bottom="180" 
             Width="60" Height="60" 
             Fill="Green"/>
</Canvas>
```

### 6.2 Drawing Application

```xml
<Canvas Background="White">
    <!-- วาดบ้าน -->
    <!-- ตัวบ้าน -->
    <Rectangle Canvas.Left="150" Canvas.Top="200" 
               Width="200" Height="150" 
               Fill="Beige" 
               Stroke="Black" 
               StrokeThickness="2"/>
    
    <!-- หลังคา -->
    <Polygon Canvas.Left="150" Canvas.Top="200"
             Points="0,0 100,-80 200,0" 
             Fill="Red" 
             Stroke="Black" 
             StrokeThickness="2"/>
    
    <!-- ประตู -->
    <Rectangle Canvas.Left="220" Canvas.Top="270" 
               Width="60" Height="80" 
               Fill="Brown"/>
    
    <!-- หน้าต่าง -->
    <Rectangle Canvas.Left="170" Canvas.Top="220" 
               Width="50" Height="50" 
               Fill="LightBlue" 
               Stroke="Black" 
               StrokeThickness="2"/>
</Canvas>
```

### 6.3 Interactive Diagram

```xml
<Canvas Background="#F0F0F0">
    <!-- Node 1 -->
    <Ellipse Canvas.Left="100" Canvas.Top="100" 
             Width="80" Height="80" 
             Fill="LightBlue" 
             Stroke="Blue" 
             StrokeThickness="3"
             Canvas.ZIndex="2"/>
    <TextBlock Canvas.Left="125" Canvas.Top="130" 
               Text="Start" 
               Canvas.ZIndex="3"/>
    
    <!-- Arrow Line -->
    <Line Canvas.Left="180" Canvas.Top="140" 
          X1="0" Y1="0" X2="120" Y2="0" 
          Stroke="Black" 
          StrokeThickness="2"
          Canvas.ZIndex="1"/>
    
    <!-- Node 2 -->
    <Ellipse Canvas.Left="300" Canvas.Top="100" 
             Width="80" Height="80" 
             Fill="LightGreen" 
             Stroke="Green" 
             StrokeThickness="3"
             Canvas.ZIndex="2"/>
    <TextBlock Canvas.Left="330" Canvas.Top="130" 
               Text="End" 
               Canvas.ZIndex="3"/>
</Canvas>
```

---

## ส่วนที่ 7: Canvas vs Grid (25:00 - 28:00)

### เมื่อไหร่ควรใช้ Canvas vs Grid?

**ใช้ Canvas เมื่อ:**
- ต้องการควบคุมตำแหน่งแบบแม่นยำ
- วาดรูป, กราฟ, แผนภูมิ
- ทำ Game หรือ Animation
- สร้าง Drawing Application
- ต้องการ Absolute Positioning

**ใช้ Grid เมื่อ:**
- สร้าง UI ทั่วไป (Form, Layout)
- ต้องการ Responsive Design
- ต้องการ Auto Layout
- User Interface ที่ต้อง Resize ได้

**ตัวอย่างเปรียบเทียบ:**

**Grid ดีกว่า:**
```xml
<Grid>
    <Grid.RowDefinitions>
        <RowDefinition Height="*"/>
        <RowDefinition Height="*"/>
    </Grid.RowDefinitions>
    <!-- Auto resize ตาม Window -->
</Grid>
```

**Canvas ดีกว่า:**
```xml
<Canvas>
    <!-- วาดโลโก้ที่ต้องการตำแหน่งแน่นอน -->
    <Path Data="..." Canvas.Left="100" Canvas.Top="50"/>
</Canvas>
```

---

## ส่วนที่ 8: Tips & Best Practices (28:00 - 31:00)

### 8.1 กำหนดขนาด Canvas

```xml
<!-- ✅ ดี: กำหนดขนาดชัดเจน -->
<Canvas Width="800" Height="600" Background="White">
    <!-- Content -->
</Canvas>

<!-- ⚠️ ระวัง: ไม่กำหนดขนาด Element อาจหาย -->
<Canvas>
    <Ellipse Canvas.Left="100" Canvas.Top="100"/>  <!-- ไม่มี Width/Height -->
</Canvas>
```

### 8.2 ใช้ ZIndex อย่างมีระบบ

```xml
<!-- ✅ ดี: แบ่ง Layer ชัดเจน -->
<Canvas>
    <Rectangle Fill="..." Canvas.ZIndex="0"/>  <!-- Background -->
    <Ellipse Fill="..." Canvas.ZIndex="5"/>    <!-- Objects -->
    <TextBlock Text="..." Canvas.ZIndex="10"/> <!-- Text/UI -->
</Canvas>
```

### 8.3 Performance

- Canvas เร็วกว่า Panel อื่นๆ เพราะไม่ต้องคำนวณ Layout
- เหมาะกับการมี Element เยอะๆ (เช่น Game)
- ไม่รองรับ Responsive Design ธรรมดา

### 8.4 ใช้ร่วมกับ Panel อื่น

```xml
<DockPanel>
    <Border DockPanel.Dock="Top" Height="50">
        <!-- Header -->
    </Border>
    
    <!-- Canvas สำหรับ Drawing Area -->
    <Canvas Background="White">
        <!-- Drawing elements -->
    </Canvas>
</DockPanel>
```

---

## ส่วนที่ 9: Wrap Up และ Outro (31:00 - 33:00)

**สรุปสิ่งที่เราได้เรียนรู้วันนี้:**

1. ✅ Canvas คือ Panel สำหรับ Absolute Positioning
2. ✅ Canvas.Left, Canvas.Top - กำหนดตำแหน่งจากซ้าย/บน
3. ✅ Canvas.Right, Canvas.Bottom - กำหนดตำแหน่งจากขวา/ล่าง
4. ✅ Canvas.ZIndex - ควบคุม Layer (ชั้น)
5. ✅ เหมาะสำหรับ Drawing, Game, Animation
6. ✅ เปรียบเทียบกับ Grid

**Canvas เหมาะสำหรับ:**
- Drawing Applications
- Games และ Animations
- Diagrams และ Charts
- ทุกอย่างที่ต้องการตำแหน่งแม่นยำ

**จุดเด่นของ Canvas:**
- ควบคุมตำแหน่งได้ 100%
- Performance ดี (ไม่ต้องคำนวณ Layout)
- เหมาะกับ Graphics

**ในตอนต่อไป:**

เราจะมาเรียนรู้เกี่ยวกับ **UniformGrid** ซึ่งเป็น Panel ที่สร้าง Grid 
โดยทุก Cell มีขนาดเท่ากันหมด เหมาะสำหรับ Photo Gallery, Icon Grid!

**อย่าลืม:**
- กด Like ถ้าชอบ
- Subscribe เพื่อติดตามตอนต่อไป
- Comment บอกว่าอยากเรียนเรื่องอะไรต่อไป

**ขอบคุณที่รับชมครับ แล้วพบกันใหม่ตอนหน้า สวัสดีครับ!**

---

## เอกสารอ้างอิง

### Official Documentation
- [Canvas Class - Microsoft Docs](https://docs.microsoft.com/en-us/dotnet/api/system.windows.controls.canvas)
- [Panels Overview - Microsoft Docs](https://docs.microsoft.com/en-us/dotnet/desktop/wpf/controls/panels-overview)

### Properties Reference
```
Canvas.Left: Double (ระยะจากซ้าย)
Canvas.Top: Double (ระยะจากบน)
Canvas.Right: Double (ระยะจากขวา)
Canvas.Bottom: Double (ระยะจากล่าง)
Canvas.ZIndex: Int32 (Layer, Default=0)
```

---

## Tips & Best Practices

1. **Fixed Size**: Canvas มักต้องกำหนดขนาดชัดเจน
2. **ZIndex Organization**: แบ่ง Layer เป็นกลุ่มๆ (0-9 Background, 10-19 Objects, etc.)
3. **Performance**: Canvas เร็วที่สุดในบรรดา Panel ทั้งหมด
4. **Not Responsive**: Canvas ไม่เหมาะกับ Responsive UI

---

## Common Mistakes (ข้อผิดพลาดที่พบบ่อย)

### ❌ ลืมกำหนด Width/Height
```xml
<!-- ผิด: Element ไม่มีขนาด -->
<Canvas>
    <Ellipse Canvas.Left="100" Canvas.Top="100"/>
</Canvas>
```

### ✅ ถูกต้อง
```xml
<Canvas>
    <Ellipse Canvas.Left="100" Canvas.Top="100" 
             Width="80" Height="80" 
             Fill="Red"/>
</Canvas>
```

### ❌ ใช้ Canvas สำหรับ Form UI
```xml
<!-- ผิด: ไม่ Responsive -->
<Canvas>
    <TextBlock Canvas.Left="10" Canvas.Top="10" Text="Name:"/>
    <TextBox Canvas.Left="100" Canvas.Top="10" Width="200"/>
</Canvas>
```

### ✅ ถูกต้อง - ใช้ Grid แทน
```xml
<Grid>
    <Grid.ColumnDefinitions>
        <ColumnDefinition Width="Auto"/>
        <ColumnDefinition Width="*"/>
    </Grid.ColumnDefinitions>
    <TextBlock Grid.Column="0" Text="Name:"/>
    <TextBox Grid.Column="1"/>
</Grid>
```

---

## Code Examples Repository

Source code สำหรับ Episode นี้สามารถดาวน์โหลดได้ที่:
- GitHub: [WPF_Episode07_Canvas](https://github.com/koson/WPF_Episode07_Canvas)

---

**End of Script**