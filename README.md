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

![image](https://github.com/codepks/LearningWPF/assets/17923311/6fd42592-989e-405d-9091-23896dd013fb)

6. But 2nd degree of stacking would not equally divide our grid, so we can achieve this using **Grid** and **ColumnDefinitions**
- First make the column definition
- put buttons inside the column definition 
```
<StackPanel>
    <Grid >
        <Grid.ColumnDefinitions>
            <ColumnDefinition Width="*"/>
            <ColumnDefinition Width="*"/>
            <ColumnDefinition Width="*"/>
        </Grid.ColumnDefinitions>

        <Button Grid.Column="0" Content="Apply"/>
        <Button Grid.Column="1" Content="Reset"/>
        <Button Grid.Column="2" Content="Refresh"/>
    </Grid>
</StackPanel>
```
**"*"** denotes the equal ration thing when diving the column width wise

7. Overall Padding : To put a good padding around whole code we can use **<Border Padding = " ">**
```
<Border Padding="10">
<StackPanel>
    <Grid >
```

8. To put padding around the buttons, we can use **Margin** inside the buttons
```
<Button Margin="10 0 10 0" Grid.Column="0" Content="Apply"/>
```
9. Note : Padding goes inside whereas margin goes outside.

10. To increase the size of textbox we can use padding instead of margin(which will reduce its size)

11. In this example we mostly decide between StackPanel or Grid. If there is more than one element in row then it would be Grid else STackPAnel in case of StackPanel.

12. In order to enter multiple elements in rows and columns (it cnabe visually identified) make a grid and add row and column definitions
    - In general start with Grid.ColumnDefinitions and within column one can add stack of items

13. For combo box and selecting the default one:
```
<ComboBox Padding="2" SelectedIndex="0" Margin="0 0 0 10" >
    <ComboBoxItem>Rubber</ComboBoxItem>
    <ComboBoxItem>Not Rubber</ComboBoxItem>
</ComboBox>
```

14. Events for Button is **Checked** and for Checkbox is **Checked**













