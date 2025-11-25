# 📝 Episode 07: Canvas - Quick Reference

> **Problem**: Other panels auto-arrange elements. What if you need **pixel-perfect positioning**?
> 
> **Solution**: **Canvas** - Absolute positioning with X, Y coordinates!

---

## 🎯 The Problem Canvas Solves

### Scenario: Drawing Application

You're building a **drawing app** where users drag shapes around:

```xml
<!-- ❌ StackPanel: Elements stack automatically -->
<StackPanel>
    <Ellipse Width="50" Height="50"/>  <!-- Always stacks vertically -->
    <Rectangle Width="60" Height="40"/> <!-- Can't position freely -->
</StackPanel>

<!-- ❌ Grid: Need row/column definitions -->
<Grid>
    <!-- Too rigid, can't place at arbitrary positions -->
</Grid>

<!-- ❌ DockPanel: Only edge docking -->
<DockPanel>
    <!-- Limited to Top/Bottom/Left/Right -->
</DockPanel>
```

**Problem:**
- **All panels auto-arrange** - You can't place elements at exact pixel positions
- **Need pixel-perfect control** for drawing, games, animations
- **Want absolute positioning** like drawing on canvas

### Canvas Solution

```xml
<Canvas Width="400" Height="300" Background="White">
    <!-- Place at exact coordinates! -->
    <Ellipse Canvas.Left="100" Canvas.Top="50" 
             Width="80" Height="80" 
             Fill="Red"/>
    
    <Rectangle Canvas.Left="200" Canvas.Top="150" 
               Width="100" Height="60" 
               Fill="Blue"/>
    
    <Ellipse Canvas.Left="50" Canvas.Top="200" 
             Width="60" Height="60" 
             Fill="Green"/>
</Canvas>
```

**Benefits:**
- ✅ **Pixel-perfect positioning** - Place at exact X, Y coordinates
- ✅ **No auto-arrangement** - You control everything
- ✅ **Perfect for drawing** - Like drawing on paper
- ✅ **Great performance** - No layout calculations
- ✅ **Layering control** - Z-Index for overlapping

---

## 📚 Canvas Basics

### What is Canvas?

**Canvas** = Layout panel with **absolute positioning**

Think of it like:
- **Drawing on paper** - You place each shape at exact positions
- **Coordinate system** - X (horizontal), Y (vertical)
- **Origin (0,0)** at top-left corner

### Key Concept: Absolute Positioning

```
Canvas coordinate system:

(0,0) ────────────► X (Left)
  │
  │
  │
  │
  ▼
  Y (Top)
```

**Other panels:** Automatic layout (stack, grid, dock)  
**Canvas:** Manual layout (you specify X, Y)

---

## 🧭 Canvas Attached Properties

### Canvas.Left and Canvas.Top

Most commonly used properties:

```xml
<Canvas>
    <Ellipse Canvas.Left="100" Canvas.Top="50" 
             Width="80" Height="80" 
             Fill="Red"/>
</Canvas>
```

**Canvas.Left** - Distance from **left edge** (X coordinate)  
**Canvas.Top** - Distance from **top edge** (Y coordinate)

```
Canvas (400×300)
┌─────────────────────────────┐
│                             │
│     (100, 50)               │
│        ●                    │ ← Ellipse at Left=100, Top=50
│                             │
│                             │
└─────────────────────────────┘
```

### Canvas.Right and Canvas.Bottom

Alternative positioning from opposite edges:

```xml
<Canvas Width="400" Height="300">
    <!-- Position from right edge -->
    <Ellipse Canvas.Right="50" Canvas.Top="50" 
             Width="70" Height="70" 
             Fill="Purple"/>
    
    <!-- Position from bottom edge -->
    <Rectangle Canvas.Left="50" Canvas.Bottom="50" 
               Width="80" Height="60" 
               Fill="Orange"/>
    
    <!-- Position from right-bottom corner -->
    <Ellipse Canvas.Right="50" Canvas.Bottom="50" 
             Width="60" Height="60" 
             Fill="Green"/>
</Canvas>
```

**Canvas.Right** - Distance from **right edge**  
**Canvas.Bottom** - Distance from **bottom edge**

**Note:**
- Use either **Left** OR **Right** (not both)
- Use either **Top** OR **Bottom** (not both)
- Most common: **Left + Top**

### Canvas.ZIndex

Control **layering** when elements overlap:

```xml
<Canvas>
    <!-- Blue rectangle (ZIndex=5) -->
    <Rectangle Canvas.Left="100" Canvas.Top="100" 
               Width="150" Height="100" 
               Fill="Blue"
               Canvas.ZIndex="5"/>
    
    <!-- Red rectangle (ZIndex=10) appears ON TOP -->
    <Rectangle Canvas.Left="150" Canvas.Top="130" 
               Width="150" Height="100" 
               Fill="Red"
               Canvas.ZIndex="10"/>
</Canvas>
```

**How ZIndex works:**
- **Higher ZIndex** = On top (closer to viewer)
- **Lower ZIndex** = Below
- **Default ZIndex** = 0
- If same ZIndex, **last element** in XAML is on top

Think of it like **layers in Photoshop**:
```
┌─────────────────┐
│  ZIndex = 10    │ ← Top layer (Red)
├─────────────────┤
│  ZIndex = 5     │ ← Middle layer (Blue)
├─────────────────┤
│  ZIndex = 0     │ ← Bottom layer (Background)
└─────────────────┘
```

---

## 💡 Common Patterns

### Pattern 1: Drawing Shapes

```xml
<Canvas Width="500" Height="400" Background="White">
    <!-- Circle -->
    <Ellipse Canvas.Left="50" Canvas.Top="50" 
             Width="80" Height="80" 
             Fill="Red" 
             Stroke="Black" 
             StrokeThickness="2"/>
    
    <!-- Rectangle -->
    <Rectangle Canvas.Left="200" Canvas.Top="100" 
               Width="120" Height="80" 
               Fill="Blue" 
               Stroke="Black" 
               StrokeThickness="2"/>
    
    <!-- Line -->
    <Line Canvas.Left="100" Canvas.Top="250" 
          X1="0" Y1="0" X2="150" Y2="50" 
          Stroke="Green" 
          StrokeThickness="3"/>
    
    <!-- Text -->
    <TextBlock Canvas.Left="350" Canvas.Top="200" 
               Text="Canvas Demo" 
               FontSize="20" 
               FontWeight="Bold"/>
</Canvas>
```

### Pattern 2: Game Scene

```xml
<Canvas Width="600" Height="400" Background="SkyBlue">
    <!-- Sun (top-right) -->
    <Ellipse Canvas.Right="50" Canvas.Top="50" 
             Width="80" Height="80" 
             Fill="Yellow"
             Canvas.ZIndex="1"/>
    
    <!-- Ground (bottom) -->
    <Rectangle Canvas.Left="0" Canvas.Bottom="0" 
               Width="600" Height="100" 
               Fill="Green"
               Canvas.ZIndex="0"/>
    
    <!-- Player (on ground) -->
    <Rectangle Canvas.Left="100" Canvas.Bottom="100" 
               Width="40" Height="60" 
               Fill="Red"
               Canvas.ZIndex="10"/>
    
    <!-- Tree trunk -->
    <Rectangle Canvas.Left="300" Canvas.Bottom="100" 
               Width="20" Height="80" 
               Fill="Brown"
               Canvas.ZIndex="5"/>
    
    <!-- Tree foliage -->
    <Ellipse Canvas.Left="280" Canvas.Bottom="180" 
             Width="60" Height="60" 
             Fill="DarkGreen"
             Canvas.ZIndex="5"/>
</Canvas>
```

### Pattern 3: Diagram with Nodes

```xml
<Canvas Width="500" Height="300" Background="#F5F5F5">
    <!-- Node 1 -->
    <Ellipse Canvas.Left="100" Canvas.Top="100" 
             Width="80" Height="80" 
             Fill="LightBlue" 
             Stroke="Blue" 
             StrokeThickness="3"
             Canvas.ZIndex="2"/>
    <TextBlock Canvas.Left="120" Canvas.Top="130" 
               Text="Start" 
               FontWeight="Bold"
               Canvas.ZIndex="3"/>
    
    <!-- Arrow (connecting line) -->
    <Line Canvas.Left="180" Canvas.Top="140" 
          X1="0" Y1="0" X2="120" Y2="0" 
          Stroke="Black" 
          StrokeThickness="2"
          StrokeEndLineCap="Triangle"
          Canvas.ZIndex="1"/>
    
    <!-- Node 2 -->
    <Ellipse Canvas.Left="300" Canvas.Top="100" 
             Width="80" Height="80" 
             Fill="LightGreen" 
             Stroke="Green" 
             StrokeThickness="3"
             Canvas.ZIndex="2"/>
    <TextBlock Canvas.Left="325" Canvas.Top="130" 
               Text="End" 
               FontWeight="Bold"
               Canvas.ZIndex="3"/>
</Canvas>
```

### Pattern 4: Drawing a House

```xml
<Canvas Width="400" Height="400" Background="LightSkyBlue">
    <!-- House body -->
    <Rectangle Canvas.Left="150" Canvas.Top="200" 
               Width="200" Height="150" 
               Fill="Beige" 
               Stroke="Black" 
               StrokeThickness="2"
               Canvas.ZIndex="1"/>
    
    <!-- Roof (triangle) -->
    <Polygon Canvas.Left="150" Canvas.Top="200"
             Points="0,0 100,-80 200,0" 
             Fill="Red" 
             Stroke="Black" 
             StrokeThickness="2"
             Canvas.ZIndex="2"/>
    
    <!-- Door -->
    <Rectangle Canvas.Left="220" Canvas.Top="270" 
               Width="60" Height="80" 
               Fill="Brown"
               Canvas.ZIndex="3"/>
    
    <!-- Window -->
    <Rectangle Canvas.Left="170" Canvas.Top="220" 
               Width="50" Height="50" 
               Fill="LightBlue" 
               Stroke="Black" 
               StrokeThickness="2"
               Canvas.ZIndex="3"/>
    
    <!-- Ground -->
    <Rectangle Canvas.Left="0" Canvas.Top="350" 
               Width="400" Height="50" 
               Fill="Green"
               Canvas.ZIndex="0"/>
</Canvas>
```

---

## ⚖️ Canvas vs Other Panels

### When to Use Canvas

✅ **Use Canvas for:**
- Drawing applications
- Games and animations
- Charts and diagrams
- Custom graphics
- Pixel-perfect positioning needed
- Elements don't need to resize with window

**Example:**
```xml
<Canvas Width="800" Height="600">
    <!-- Game sprites at exact positions -->
    <Image Canvas.Left="100" Canvas.Top="200" Source="player.png"/>
    <Image Canvas.Left="300" Canvas.Top="150" Source="enemy.png"/>
</Canvas>
```

### When NOT to Use Canvas

❌ **Don't use Canvas for:**
- Form layouts (use Grid)
- Responsive UI (use Grid, StackPanel, DockPanel)
- General application UI
- Automatic resizing needed

**Example - Use Grid instead:**
```xml
<!-- ❌ Bad: Canvas for forms -->
<Canvas>
    <TextBlock Canvas.Left="10" Canvas.Top="10" Text="Name:"/>
    <TextBox Canvas.Left="100" Canvas.Top="10" Width="200"/>
</Canvas>

<!-- ✅ Good: Grid for forms -->
<Grid>
    <Grid.ColumnDefinitions>
        <ColumnDefinition Width="Auto"/>
        <ColumnDefinition Width="*"/>
    </Grid.ColumnDefinitions>
    <TextBlock Grid.Column="0" Text="Name:"/>
    <TextBox Grid.Column="1"/>
</Grid>
```

### Comparison Table

| Feature | Canvas | Grid | StackPanel | DockPanel |
|---------|--------|------|------------|-----------|
| **Positioning** | Absolute (X, Y) | Row/Column | Sequential | Edge-docking |
| **Responsive** | ❌ No | ✅ Yes | ✅ Yes | ✅ Yes |
| **Overlapping** | ✅ Yes (ZIndex) | ✅ Yes (same cell) | ❌ No | ❌ No |
| **Auto Layout** | ❌ No | ✅ Yes | ✅ Yes | ✅ Yes |
| **Performance** | ✅ Fastest | ⚡ Good | ⚡ Good | ⚡ Good |
| **Use Case** | Drawing, Games | Forms, UI | Lists | App layout |

---

## 🎨 Advanced Techniques

### Technique 1: Layered Drawing

Use ZIndex to create depth:

```xml
<Canvas Width="400" Height="300">
    <!-- Background layer (ZIndex 0) -->
    <Rectangle Canvas.Left="0" Canvas.Top="0" 
               Width="400" Height="300" 
               Fill="#F0F0F0"
               Canvas.ZIndex="0"/>
    
    <!-- Shadow layer (ZIndex 1-4) -->
    <Ellipse Canvas.Left="105" Canvas.Top="105" 
             Width="80" Height="80" 
             Fill="Gray" 
             Opacity="0.3"
             Canvas.ZIndex="1"/>
    
    <!-- Object layer (ZIndex 5-9) -->
    <Ellipse Canvas.Left="100" Canvas.Top="100" 
             Width="80" Height="80" 
             Fill="Red"
             Canvas.ZIndex="5"/>
    
    <!-- UI layer (ZIndex 10+) -->
    <TextBlock Canvas.Left="130" Canvas.Top="130" 
               Text="🎯" 
               FontSize="24"
               Canvas.ZIndex="10"/>
</Canvas>
```

**Layer Organization:**
- **0-4**: Background, shadows
- **5-9**: Objects
- **10+**: UI elements, text

### Technique 2: Combining with Other Panels

Canvas works great inside other panels:

```xml
<DockPanel>
    <!-- Toolbar at top -->
    <Border DockPanel.Dock="Top" Height="50" Background="LightGray">
        <StackPanel Orientation="Horizontal">
            <Button Content="Draw Circle" Margin="5"/>
            <Button Content="Draw Rectangle" Margin="5"/>
            <Button Content="Clear" Margin="5"/>
        </StackPanel>
    </Border>
    
    <!-- Canvas as main drawing area -->
    <Canvas Background="White">
        <!-- User draws here -->
    </Canvas>
</DockPanel>
```

### Technique 3: Centered Elements

Canvas doesn't auto-center, but you can calculate:

```xml
<Canvas Width="400" Height="300" Background="White">
    <!-- Center a 100x100 element -->
    <!-- Left = (CanvasWidth - ElementWidth) / 2 = (400 - 100) / 2 = 150 -->
    <!-- Top = (CanvasHeight - ElementHeight) / 2 = (300 - 100) / 2 = 100 -->
    <Rectangle Canvas.Left="150" Canvas.Top="100" 
               Width="100" Height="100" 
               Fill="Blue"/>
</Canvas>
```

**Formula:**
```
CenterX = (CanvasWidth - ElementWidth) / 2
CenterY = (CanvasHeight - ElementHeight) / 2
```

---

## ⚠️ Common Problems & Solutions

### Problem 1: Element Not Visible

```xml
<!-- ❌ Problem: No Width/Height specified -->
<Canvas>
    <Ellipse Canvas.Left="100" Canvas.Top="100" Fill="Red"/>
    <!-- Element has no size! Won't show! -->
</Canvas>

<!-- ✅ Solution: Always specify size -->
<Canvas>
    <Ellipse Canvas.Left="100" Canvas.Top="100" 
             Width="80" Height="80" 
             Fill="Red"/>
</Canvas>
```

### Problem 2: Wrong Layering

```xml
<!-- ❌ Problem: Element written last appears on top (unwanted) -->
<Canvas>
    <Ellipse Canvas.Left="100" Canvas.Top="100" 
             Width="100" Height="100" 
             Fill="Red"/>
    
    <Rectangle Canvas.Left="120" Canvas.Top="120" 
               Width="80" Height="80" 
               Fill="Blue"/>
    <!-- Blue appears ON TOP of Red (written last) -->
</Canvas>

<!-- ✅ Solution: Use ZIndex explicitly -->
<Canvas>
    <Ellipse Canvas.Left="100" Canvas.Top="100" 
             Width="100" Height="100" 
             Fill="Red"
             Canvas.ZIndex="10"/>  <!-- Higher = on top -->
    
    <Rectangle Canvas.Left="120" Canvas.Top="120" 
               Width="80" Height="80" 
               Fill="Blue"
               Canvas.ZIndex="5"/>   <!-- Lower = below -->
    <!-- Now Red is on top! -->
</Canvas>
```

### Problem 3: Canvas Not Resizing

```xml
<!-- ❌ Problem: Canvas size not specified, elements may clip -->
<Canvas>
    <Ellipse Canvas.Left="500" Canvas.Top="500" 
             Width="80" Height="80" 
             Fill="Red"/>
    <!-- Might be clipped if Canvas is smaller! -->
</Canvas>

<!-- ✅ Solution: Specify Canvas size -->
<Canvas Width="600" Height="600" Background="White">
    <Ellipse Canvas.Left="500" Canvas.Top="500" 
             Width="80" Height="80" 
             Fill="Red"/>
    <!-- Now Canvas is big enough! -->
</Canvas>
```

### Problem 4: Using Canvas for Forms

```xml
<!-- ❌ Bad: Canvas for form layout (not responsive) -->
<Canvas>
    <TextBlock Canvas.Left="10" Canvas.Top="10" Text="Name:"/>
    <TextBox Canvas.Left="100" Canvas.Top="10" Width="200"/>
    <TextBlock Canvas.Left="10" Canvas.Top="50" Text="Email:"/>
    <TextBox Canvas.Left="100" Canvas.Top="50" Width="200"/>
    <!-- Fixed positions, won't adapt to window size -->
</Canvas>

<!-- ✅ Good: Use Grid for forms -->
<Grid Margin="10">
    <Grid.RowDefinitions>
        <RowDefinition Height="Auto"/>
        <RowDefinition Height="Auto"/>
    </Grid.RowDefinitions>
    <Grid.ColumnDefinitions>
        <ColumnDefinition Width="Auto"/>
        <ColumnDefinition Width="*"/>
    </Grid.ColumnDefinitions>
    
    <TextBlock Grid.Row="0" Grid.Column="0" Text="Name:" Margin="5"/>
    <TextBox Grid.Row="0" Grid.Column="1" Margin="5"/>
    <TextBlock Grid.Row="1" Grid.Column="0" Text="Email:" Margin="5"/>
    <TextBox Grid.Row="1" Grid.Column="1" Margin="5"/>
    <!-- Responsive, adapts to window size -->
</Grid>
```

---

## 💪 Best Practices

### Do's ✅

1. **Specify Canvas size** for predictable behavior
   ```xml
   <Canvas Width="800" Height="600" Background="White">
   ```

2. **Always specify element size** (Width, Height)
   ```xml
   <Ellipse Width="80" Height="80" Fill="Red"/>
   ```

3. **Use ZIndex systematically** for layering
   ```xml
   <!-- Background: 0-4, Objects: 5-9, UI: 10+ -->
   <Rectangle Canvas.ZIndex="0"/>  <!-- Background -->
   <Ellipse Canvas.ZIndex="5"/>    <!-- Object -->
   <TextBlock Canvas.ZIndex="10"/> <!-- UI -->
   ```

4. **Organize ZIndex by purpose**
   - 0-4: Backgrounds, shadows
   - 5-9: Main objects
   - 10+: UI elements, text, overlays

5. **Use for drawing/games**, not forms

### Don'ts ❌

1. **Don't use for general UI**
   - Use Grid, StackPanel, DockPanel instead

2. **Don't forget element sizes**
   - Always specify Width and Height

3. **Don't rely on XAML order for layering**
   - Use explicit ZIndex instead

4. **Don't expect responsive behavior**
   - Canvas uses fixed positioning

5. **Don't use for layouts that need to resize**
   - Canvas elements stay at fixed positions

---

## 📋 Quick Reference

### Canvas Attached Properties

```xml
<Canvas>
    <!-- Position from edges -->
    <Element Canvas.Left="100"/>    <!-- Distance from left -->
    <Element Canvas.Top="50"/>      <!-- Distance from top -->
    <Element Canvas.Right="50"/>    <!-- Distance from right -->
    <Element Canvas.Bottom="30"/>   <!-- Distance from bottom -->
    
    <!-- Layer control -->
    <Element Canvas.ZIndex="10"/>   <!-- Higher = on top -->
</Canvas>
```

### Common Element Types

```xml
<Canvas>
    <!-- Shapes -->
    <Ellipse Width="80" Height="80" Fill="Red"/>
    <Rectangle Width="100" Height="60" Fill="Blue"/>
    <Line X1="0" Y1="0" X2="100" Y2="100" Stroke="Black"/>
    <Polygon Points="0,0 50,100 100,0" Fill="Green"/>
    
    <!-- Text -->
    <TextBlock Text="Hello" FontSize="20"/>
    
    <!-- Images -->
    <Image Source="image.png" Width="100" Height="100"/>
</Canvas>
```

### ZIndex Hierarchy

```
Higher ZIndex (on top)
    ↑
    │  10+  UI elements, text, overlays
    │  5-9  Main objects, shapes
    │  1-4  Shadows, effects
    │  0    Background
    ↓
Lower ZIndex (below)
```

---

## 🎯 Summary

**Canvas** is the panel for **absolute positioning**:

| Aspect | Description |
|--------|-------------|
| **Purpose** | Pixel-perfect positioning |
| **Positioning** | Absolute (X, Y coordinates) |
| **Layout** | Manual (you control everything) |
| **Best For** | Drawing, games, animations, diagrams |
| **Avoid For** | Forms, general UI, responsive layouts |
| **Key Properties** | Canvas.Left, Canvas.Top, Canvas.ZIndex |
| **Performance** | ✅ Fastest (no layout calculation) |

**When to use:**
- ✅ Drawing applications
- ✅ Games
- ✅ Charts/diagrams
- ✅ Need pixel-perfect control

**When NOT to use:**
- ❌ Forms and data entry
- ❌ Responsive UI
- ❌ General application layout

---

## 🔗 Related

- **Alternative**: [Episode 04 - Grid](../WPF_Episode04_Grid) - For table layouts
- **Complement**: [Episode 06 - DockPanel](../WPF_Episode06_DockPanel) - For app shells
- **Next**: [Episode 08 - UniformGrid](../WPF_Episode08_UniformGrid) - Equal-sized cells

---

*For complete examples, see [README.md](README.md)*
