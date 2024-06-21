# Starting
MainWindow.xaml is the xaml file to start with.

# Basics
```
<Button FontWeight="Bold" Content="A button" />
```

The above code can be written in **Control-Dot-Property** notation

```
<Button>
    <Button.FontWeight>Bold</Button.FontWeight>
    <Button.Content>A button</Button.Content>
</Button>
```

## WrapPanel
The Content property only allows for a single child element, so we use a WrapPanel to contain the differently colored blocks of text.
```
<Button>
    <Button.FontWeight>Bold</Button.FontWeight>
    <Button.Content>
        <WrapPanel>
            <TextBlock Foreground="Blue">Multi</TextBlock>
            <TextBlock Foreground="Red">Color</TextBlock>
            <TextBlock>Button</TextBlock>
        </WrapPanel>
    </Button.Content>
</Button>
```

# WPF Tutorial
![image](https://github.com/codepks/LearningWPF/assets/17923311/4e708224-ac44-4500-9b73-433519d3e12d)

1. Create **WPF Application** from the Visual Studio
2. We will start by putting the elements in **stackPanel** to stack the elements one after the another
3. Change the <Grid> to **<StackPanel>** as it puts the elements one above the another
```
<StackPanel>
    <Button Content="Test"/>
    <Button Content="Test"/>
    <Button Content="Test"/> 
</StackPanel>
```
4.  **<Grid>** on the other hands puts the elements in overlap as Grid is one element or one row thing
```
<Grid>
    <Button Content="Test"/>
    <Button Content="Test"/>
    <Button Content="Test"/>
</Grid>
```
5. In the above requirement, we need two degrees of stackPanel one for the outer for stacking up groups and one for the elements
![image](https://github.com/codepks/LearningWPF/assets/17923311/675d8c8e-bff9-48c3-bd71-d1bff6d71a8c)

6. 














