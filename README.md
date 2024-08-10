# Starting
MainWindow.xaml is the xaml file to start with.

1. In MVVM we try not to keep any logic in view (.xaml and .xaml.cs(code-behind))
2. Instead we keep the logic in View Model and bind the View Model elements to the view

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

# WPF Tutorial - Chapter 1 - Static UI and Event Handling
![image](https://github.com/codepks/LearningWPF/assets/17923311/4e708224-ac44-4500-9b73-433519d3e12d)

[source](https://www.youtube.com/watch?v=Vjldip84CXQ&list=PLrW43fNmjaQVYF4zgsD0oL9Iv6u23PI6M&index=1&ab_channel=AngelSix)

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

14. For adding controller to the element be it button or checkbox you need to have its listener in the source code and a controller which you mention with the name of the checkbox using **x:Name=""**

15. On Adding events like **Click** and **Checked** the source code will automatically add the listener function in source code through which the events will be recieved. You can adjust the name to make it customized as per your needs.

In the code below we are trying to display some text on the Desciption box on click of apply button
_xaml code_
```
 <TextBox x:Name="DescriptionTextBox" Padding="2"/>

 <Button x:Name="ApplyButton" Click="ApplyButton_Click" Margin="0 0 10 0" Grid.Column="0" Content="Apply" />
```
_added source code_
```
 private void Apply_Button_Click(object sender, RoutedEventArgs e)
 {
     this.DescriptionTextBox.Text = "Apply Button Clicked";
 }
```


16. **Events**
    -  for Button is **Click** and
    -  for Checkbox is **Checked**

17. The **xName** given is a controlled and can be accessed via
```
this.TextController
```
18. How to get the handle of the element from the listener function:
```
private void Checkbox_Checked(object sender, RoutedEventArgs e)
{
    this.LengthText.Text += ((CheckBox)sender).Content;
}
```
here **sender** is the checkbox itself (parent)which needs to be typecasted to the checkbox before being used as the type Checkbox

Note: + operator is necessary here because you _add to_ what is already in there instead of overwriting it.

19. Similary for retrieving item from Dropdown and displaying it on a TextBlock
selectionChanged is the _event handler_ here
```
<ComboBox SelectionChanged="ComboBox_SelectionChanged_Purchase"  Padding="2" SelectedIndex="0" Margin="0 0 0 10" >
    <ComboBoxItem>Rubber</ComboBoxItem>
    <ComboBoxItem>Not Rubber</ComboBoxItem>
</ComboBox>

<TextBlock Text="Supplier Name"/>
<TextBox x:Name="PurchaseNote" Margin="0 0 0 10"/>
```

```
private void ComboBox_SelectionChanged_Purchase(object sender, SelectionChangedEventArgs e)
{
    if (PurchaseNote == null)
        return;

    var combo = (ComboBox)sender;
    var selectedValue = (ComboBoxItem)combo.SelectedValue;

    this.PurchaseNote.Text += (string)selectedValue.Content;
}
```
Note:
- We check for null as on UI load the combobox is null, so to avoid crash we check for null.
- The sequestion is :
    a. Get the combo
    b. Get the selected value as ComboItem from the combo
    c. Get the content from the ComboItem and cast it to a string

20. Task : To display on the text/checkbox/combobox on UI load or startup
    - Either one can go writing the startup code in the constructor
    - Or **override** **Loaded** function which gets called on UI load
    - You can call any of the even handler methos in this Loaded overriden method to load a content on startup of UI

21. MessageBox.Show("<string>") shows a dialog box and can be used for debugging too.


# WPF Tutorial - Chapter 2 - MVVM

[source](https://www.codeproject.com/Articles/819294/WPF-MVVM-step-by-step-Basics-to-Advance-Level)

## Introduction 
We follow basic 3 layer architecture
1. User Interface
2. Business Logic
3. Data Access Layer

## Mapping Code and Transformation Code

### Noob Code
```
lblName.Content = o.CustomerName; // mapping code or binding logic
lblAmount.Content = o.Amount; // mapping code

if (o.Amount > 2000) // transformation code
{
    lblBuyingHabits.Background = new SolidColorBrush(Colors.Blue);
}
else if (o.Amount > 1500) // transformation code
{
    lblBuyingHabits.Background = new SolidColorBrush(Colors.Red);
}

if (obj.Married == "Married") // transformation code
{
    chkMarried.IsChecked = true;
}
else
{
    chkMarried.IsChecked = false;
}
```
A normal deveoper puts both of these in code behind of XAML.cs which is basicaly a UI layer. <br>

### Responsibilities of UI layer
The reponsibility of UI layer is to only control the look and feel of UI layer and not the logic of the code.

### Problems
This may create problem in switching this code to a different technologies. For example MVC, Web or Mobile techs. <br>

The current code that we have written in XAML.cs is inheriting from WPF specific class MainWindow which is at UI layer <br>
Switching to other techs may need this to be removed. <br>


### class libraries
We can use class libraries which can have all the UI properties in a class and it can be used as a reference in some WPF projecct. <br>

## MVVM
We will separate the transformation logic to a class library which containts the UI properties and use this in mapping in the code behing
<br>
Class Library where all the properties are defined and can be re-used in other technologies too. <br>
1. Below is our **ViewModel** class as CustomerViewModel
2. Customer would be our Model class
3. CustomerViewModel would be having the Properties listed in it which wil be exposing the data members of the model class `obj.CustomerName` for e.g.
4. It will have mapping as well as the transformational code.

```
public class CustomerViewModel 
    {
        private Customer obj = new Customer();

        public string TxtCustomerName
        {
            get { return obj.CustomerName; }
            set { obj.CustomerName = value; }
        }        

        public string TxtAmount
        {
            get { return Convert.ToString(obj.Amount) ; }
            set { obj.Amount = Convert.ToDouble(value); }
        }


        public string LblAmountColor
        {
            get 
            {
                if (obj.Amount > 2000)
                {
                    return "Blue";
                }
                else if (obj.Amount > 1500)
                {
                    return "Red";
                }
                return "Yellow";
            }
        }

        public bool IsMarried
        {
            get
            {
                if (obj.Married == "Married")
                {
                    return true;
                }
                else
                {
                    return false;
                }
            }

        }}
```

Mapping logic in Code Behind
```
private void DisplayUi(CustomerViewModel o)
{
lblName.Content = o.TxtCustomerName;
lblAmount.Content = o.TxtAmount;
BrushConverter brushconv = new BrushConverter();
lblBuyingHabits.Background = brushconv.ConvertFromString(o.LblAmountColor) as SolidColorBrush;
chkMarried.IsChecked = o.IsMarried;
}
```

This is what our project should look like :
![image](https://github.com/codepks/LearningWPF/assets/17923311/e40256d4-061a-4804-9cfd-5a9f7ab4a7f7)

In the architecture abve, this is how you are going to add reference:
1. Add reference of ViewModel in View layer
2. Add reference of Model n ViewModel layer
3. View shouldn't have reference to the model direcctly

## Zeroing the code behind
We can make the code behind to zero by doing things in XAML file instead and the taking car eo the binding too

![image](https://github.com/codepks/LearningWPF/assets/17923311/f2e9fc22-7801-4f3b-a247-21f95a863a87)

If you see the behind code of your XAML.CS it has no GLUE code, neither transformation or mapping nature code. The only code which is present is the standard WPF code which initializes the main WPF UI.

```
public partial class MVVMWithBindings : Window
{
        public MVVMWithBindings()
        {InitializeComponent();}
}
```

## Adding actions and notifications

**"_ViewModel is a wrapper around the Model class._"**

1. Suppose if we make Calculate Tax button in the UI, then the model class Customber will have its implmentation
2. CustomerViewModel will take care of its invocation
```
public class CustomerViewModel 
{
        private Customer obj = new Customer();
....
....
....
....
        public void Calculate()
        {
            obj.CalculateTax();
        }
}
```

How we invoke the Calculate method from the XAML to the ViewModel class? two ways to communicate
1. We can interact from XAML to ViewModel using Properties using Bindings
2. We can also send actions to ViewModel using commands

Here we need to send commands.

### Commands
Let's make a ButtonCommand here which inherits from inherits from ICommand
```
public class ButtonCommand : ICommand
{
        public bool CanExecute(object parameter)
        {
      // When to execute
      // Validation logic goes here
        }

        public event EventHandler CanExecuteChanged;

        public void Execute(object parameter)
        {
// What to Execute
      // Execution logic goes here
    }
}
```

1. This command interface forces to implments 2 functions, `CanExecute` and `Execute` which takes care of Validation and what to execute steps.
2. In the `CanExecute` we can call the validation step put in our view model class or return `true` by default
3. In the `Execute` step we can call the `Calculate` tax function


_How to consume this command class now?_ <br>
1. We will create a private command objecct in our ModelView class
2. Invoke it using the ModelView class `this` pointer to give it the context
3. Expose the private object via `ICommand` method to the XAML so that XAML get to call it
4. So far above was the mapping step for Command for XAML 


### Getting Notifications
After sending the command we should notification of the command sent. For this
1. We need to inherit our ModelViewClass from `INotifyPropertyChanged`
2. In the `CalculateTax` function raise the event for property that is getting changed, for e.g. here it is `Tax`

```
public class CustomerViewModel : INotifyPropertyChanged // Point 1
{
….
….
        public void Calculate()
        {
            obj.CalculateTax();
            if (PropertyChanged != null) // Point 2
            {
                PropertyChanged(this,new PropertyChangedEventArgs("Tax"));
            // Point 3
            }
        }

        public event PropertyChangedEventHandler PropertyChanged;
}
```

## Making Commands Generic
We can make the commands generic and independent of which ViewModel class calls it or gets trigerred in it.

**BEFORE**
```
public class CustomerViewModel 
{
    private ButtonCommand objCommand; //  Point 1
    public CustomerViewModel()
    {
        objCommand = new ButtonCommand(this); // Point 2
    }
}
```

**AFTER**
```
public class CustomerViewModel : INotifyPropertyChanged
{
    private Customer obj = new Customer();
    private ButtonCommandobjCommand;
    public CustomerViewModel()
    {
        objCommand = new ButtonCommand(obj.CalculateTax,  obj.IsValid);
    }
}
```

We will using generic delegates `Action` and `Func` in our Command class
```
public class ButtonCommand : ICommand
{
    private Action WhattoExecute;
    private Func<bool> WhentoExecute;
    public ButtonCommand(Action What , Func<bool> When) // Point 1
    {
        WhattoExecute = What;
        WhentoExecute = When;
    }
    public bool CanExecute(object parameter)
    {
        return WhentoExecute(); // Point 2
    }
    public void Execute(object parameter)
    {
        WhattoExecute(); // Point 3
    }
}
```

# Chapter 3 - Singleton Sean
## View
### MainWindow.xaml
1. In `Grid.Resources` we define the DataTemplates
2. The `DataTemplate` we specify datatype attribute where `ModelView` is associated with `View`
3. For e.g. for the `MakeReservationViewModel`, the associated view is `MakeReservationView`.

### MainWindow.xaml.cs 
1. It is mostly empty except for InitializeComponent. That is how it should be.
2. We have mode the association and view switching available in `MainWindow.xaml`

### App.xaml.cs
Lots of services are used

# My Sample
1. view.xaml is where you design the code
2. view.cs is the code behind which should as per best practice have only InitializeCompoenent() function
3. viewModel file is the one which which interacts wwith the model class and generally implements INotifyPropertyChanged and send events to UI on updates

## INotifyPropertyChanged

### Take 1 - Understanding
1. Every view-model class that inherits `INotifyPropertyChanged` is regarded as a publisher and `xaml` code element subscribe to it using `binding`
2. On inheritance we have to implement the using using this line `public event PropertyChangedEventHandler PropertyChanged;`
3. Here `PropertyChangedEventHandler` is a delegate which is required for defining the function signature of the object subscribing to it woth specific parameter list and return type

```
class MyClass
{
    public delegate void MyDelegate(object sender, EventArgs e);

    public void MyMethod1(object sender, EventArgs e)
    {
        Console.WriteLine("Hello World 1!");
    }

   public void MyMethod2(object sender, EventArgs e)
   {
      Console.WriteLine("Hello World 2!");
   }

   public void MyMethod3(object sender, EventArgs e)
   {
      Console.WriteLine("Hello World 3!");
   }
   
   public event MyDelegate MyEvent;

    public void RaiseEvent()
    {
        MyEvent?.Invoke(this, EventArgs.Empty);
    }

    public static void Main()
    {
        MyClass myClass = new MyClass();
        myClass.MyEvent += myClass.MyMethod1;
        myClass.MyEvent += myClass.MyMethod2;
        myClass.MyEvent += myClass.MyMethod3;
        myClass.RaiseEvent();
    }
}
```
1. `MyDelegate` is a delegate to define the function which can subscribe to the event `MyEvent`
2. `MyMethod1`, `MyMethod2` and `MyMethod3` being the same signature as `MyDelegate` can subscribe to `MyEvent`
3. When `RaiseEvent` is invoked, internally `MyEvent` is invoked and the `Invoke` sends the parameters, first being the publisher class and 2nd being the arguments




### Take 2
```
public class CommonBase : INotifyPropertyChanged
   {
      public event PropertyChangedEventHandler PropertyChanged; //delegate PropertyChangedEventHandler used to declare an event

      protected void RaisePropertyChanged(String propertyName)
      {
         PropertyChangedEventHandler handler = PropertyChanged;
         if(handler != null)
            handler(this, new PropertyChangedEventArgs(propertyName));	//invoking the event by sending the arguments are publisher class name and 
      }
   }
```
`PropertyChangedEventArgs` is used to specify which property has changed

```
public class CommonBase : INotifyPropertyChanged
```
1. `INotifyPropertyChanged` interface. This interface is a standard in .NET that provides a way to notify clients (like UI elements) that a property value has changed.
2. When you change the property value in your data model, it triggers the OnPropertyChanged method, which raises the PropertyChanged event.
3. Binding to properties that doesn't implement INotifyPropertyChanged can result in memory leaks
4. If you want to send a collection of properties in form of list to the view we use `ObservableCollection`
5. `ObservableCollection` implements `INotifyPropertyChanged`, so whenever we add or remove the entries in the list the listview in the xaml gets notified



```
public event PropertyChangedEventHandler PropertyChanged;
```
1. This line declares an event named PropertyChanged. This event is of the type PropertyChangedEventHandler, which is a delegate that represents the method that will handle the PropertyChanged event.
2. According to the INotifyPropertyChanged interface, when a property value changes, this event should be raised to notify any subscribers (typically UI elements) that they need to update themselves.

```
protected void RaisePropertyChanged(String propertyName)
{
   PropertyChangedEventHandler handler = PropertyChanged;
   if(handler != null)
      handler(this, new PropertyChangedEventArgs(propertyName));
}
```
1. It takes a string parameter, propertyName, which specifies the name of the property that has changed.
2. It assigns the PropertyChanged event to a local variable handler. This is **done to prevent the event from being null during invocation** if it gets unsubscribed just before the event is raised.
3.  **The if statement** checks if handler is not null, which means there are subscribers to the event. If there are, it invokes the handler passing this (the current instance of the class) and a new instance of PropertyChangedEventArgs, initialized with the propertyName that has changed.


Usage
```
public class MyViewModel : CommonBase
{
   private string myProperty;

   public string MyProperty
   {
      get { return myProperty; }
      set
      {
         if (myProperty != value)
         {
            myProperty = value;
            RaisePropertyChanged(nameof(MyProperty)); // Notify change
         }
      }
   }
}
```


# Loaded vs OnInitialized 
1. Loaded - The Loaded event is triggered after the element is loaded, which means it is fully initialized and ready to be interacted with
- In case of multiple view the dependent loaded is called after the primary loaded
- DLL loading can happen before the UI loading and until then UI loaded is not called
- Only after clicking the UI and once user is able to see the UI the Loaded function is called
2. OnInitialized method, which is called during the initialization phase, before the element is added to the visual tree. It is apparently called before Loaded

# Attaching Button from XAML to ViewModel
xaml file
```
<Button Content="Save to Database"  
        HorizontalAlignment="Left"  
        Height="30"  
        Margin="68,843,0,0"  
        VerticalAlignment="Top"  
        Width="154"  
        Command="{Binding SaveCommand}" />
```
ViewModelFile
```
using System;  
using System.Windows.Input;  

public class MyViewModel : BaseViewModel // BaseViewModel could implement INotifyPropertyChanged  
{  
    public MyViewModel()  
    {  
        SaveCommand = new RelayCommand(SaveToDatabase, CanSaveToDatabase);  
    }  

    public ICommand SaveCommand { get; private set; }  

    private void SaveToDatabase()  
    {  
        // Logic to save to the database goes here  
        Console.WriteLine("Save to database logic executed.");  
    }  

    private bool CanSaveToDatabase()  
    {  
        // Here you can add logic to determine if the command can execute  
        return true; // or false based on actual conditions  
    }  
}  

public class RelayCommand : ICommand  
{  
    private readonly Action _execute;  
    private readonly Func<bool> _canExecute;  

    public RelayCommand(Action execute, Func<bool> canExecute = null)  
    {  
        _execute = execute;  
        _canExecute = canExecute;  
    }  

    public event EventHandler CanExecuteChanged;  

    public bool CanExecute(object parameter)  
    {  
        return _canExecute == null || _canExecute();  
    }  

    public void Execute(object parameter)  
    {  
        _execute();  
    }  

    public void RaiseCanExecuteChanged()  
    {  
        CanExecuteChanged?.Invoke(this, EventArgs.Empty);  
    }  
}
```


# Types of Grid
1. **Grid**
The Grid is the most versatile layout panel in WPF. It allows you to define rows and columns with precise control over their sizes and proportions.
```
<Grid>  
    <Grid.RowDefinitions>  
        <RowDefinition Height="Auto"/>  
        <RowDefinition Height="*"/>  
        <RowDefinition Height="50"/>  
    </Grid.RowDefinitions>  
    <Grid.ColumnDefinitions>  
        <ColumnDefinition Width="200"/>  
        <ColumnDefinition Width="*"/>  
    </Grid.ColumnDefinitions>  
    
    <TextBlock Grid.Row="0" Grid.Column="0" Text="Name:"/>  
    <TextBox Grid.Row="0" Grid.Column="1" />  
    <Button Grid.Row="1" Grid.ColumnSpan="2" Content="Submit"/>  
</Grid>
```

2. **UniformGrid**
UniformGrid arranges elements in a grid where all cells are of equal size. It takes care of distributing available space evenly across all children, making it ideal for scenarios where uniform cell sizes are preferred.
```
<UniformGrid Rows="2" Columns="2">  
    <Button Content="Button 1"/>  
    <Button Content="Button 2"/>  
    <Button Content="Button 3"/>  
    <Button Content="Button 4"/>  
</UniformGrid>
```

3. **WrapPanel** positions child elements in sequential order from left to right and wraps them to the next line when there's not enough space. It is handy if the number of items in your UI may change.
```
<WrapPanel>  
    <Button Content="Button 1"/>  
    <Button Content="Button 2"/>  
    <Button Content="Button 3"/>  
    <Button Content="Button 4"/>  
    <Button Content="Button 5"/>  
</WrapPanel>
```
4. **StackPanel** <br>
Although not a grid, a StackPanel arranges child elements into a single line, either vertically or horizontally. It’s useful for simple layouts.
```
<StackPanel Orientation="Vertical">  
    <TextBlock Text="Name:"/>  
    <TextBox/>  
    <TextBlock Text="Email:"/>  
    <TextBox/>  
</StackPanel>
```
5. **DockPanel** <br>
DockPanel allows you to dock child elements to the left, right, top, bottom, or fill the remaining space. It’s helpful for creating toolbars or menus.
```
<DockPanel>  
    <Button Content="Top" DockPanel.Dock="Top"/>  
    <Button Content="Bottom" DockPanel.Dock="Bottom"/>  
    <Button Content="Left" DockPanel.Dock="Left"/>  
    <Button Content="Right" DockPanel.Dock="Right"/>  
    <Button Content="Center"/>  
</DockPanel>
```
6. **Canvas** <br>
Canvas allows for absolute positioning of children by specifying coordinates. It’s not grid-based but useful for custom layouts where precise placement is needed.
```
<Canvas>  
    <Button Canvas.Left="50" Canvas.Top="100" Content="Button"/>  
</Canvas>
```

7. **VirtualizingStackPanel** <br>
Similar to StackPanel, but optimized for performance with large collections of items, the VirtualizingStackPanel only creates UI elements for visible items, saving memory.
```
<ListBox ItemsSource="{Binding SomeCollection}">  
    <ListBox.ItemsPanel>  
        <ItemsPanelTemplate>  
            <VirtualizingStackPanel/>  
        </ItemsPanelTemplate>  
    </ListBox.ItemsPanel>  
</ListBox>
```
8. **GridSplitter** <br>
Although it’s not a layout panel on its own, the GridSplitter can be used within a Grid to allow users to resize rows or columns interactively.
```
<Grid>  
    <Grid.RowDefinitions>  
        <RowDefinition Height="*"/>  
        <RowDefinition Height="5"/>  
        <RowDefinition Height="*"/>  
    </Grid.RowDefinitions>  
    
    <TextBlock Grid.Row="0" Text="Top Area"/>  
    <GridSplitter Grid.Row="1" />  
    <TextBlock Grid.Row="2" Text="Bottom Area"/>  
</Grid>
```

# Displaying List
Step 1: Define the Model
First, define a simple model class that will represent each row of data. For this example, we will create a model for a Person.
```
public class Person  
{  
    public string Name { get; set; }  
    public int Age { get; set; }  
}
```
Step 2: Create the ViewModel
Next, create a view model that will hold a collection of Person objects.
```
using System.Collections.ObjectModel;  

public class MainViewModel  
{  
    public ObservableCollection<Person> People { get; set; }  

    public MainViewModel()  
    {  
        People = new ObservableCollection<Person>  
        {  
            new Person { Name = "Alice", Age = 30 },  
            new Person { Name = "Bob", Age = 25 },  
            new Person { Name = "Charlie", Age = 35 }  
        };  
    }  
}
```
Step 3: Define the XAML for the View
Now, create the XAML for the MainWindow. Here, we will use a ListView to display the collection of Person objects.
```
<Window x:Class="WpfApp.MainWindow"  
        xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"  
        xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"  
        Title="People List" Height="300" Width="400">  
    <Grid>  
        <ListView ItemsSource="{Binding People}">  
            <ListView.View>  
                <GridView>  
                    <GridViewColumn Header="Name" DisplayMemberBinding="{Binding Name}" Width="200"/>  
                    <GridViewColumn Header="Age" DisplayMemberBinding="{Binding Age}" Width="100"/>  
                </GridView>  
            </ListView.View>  
        </ListView>  
    </Grid>  
</Window>
```
Step 4: Set DataContext in Code-Behind
1. Finally, set the DataContext of the MainWindow to an instance of the MainViewModel in the code-behind file (MainWindow.xaml.cs).
2. MainViewModel is the one responsible for displaying which view will be displayed in front
```
using System.Windows;  

namespace WpfApp  
{  
    public partial class MainWindow : Window  
    {  
        public MainWindow()  
        {  
            InitializeComponent();  
            DataContext = new MainViewModel(); // Set the DataContext to the ViewModel  
        }  
    }  
}
```
Summary
Model: The Person class represents a single row of data.
ViewModel: MainViewModel holds a collection of Person instances.
View: The XAML defines a ListView that binds to the People collection using a GridView to display the properties.
DataContext: The DataContext is set in the code-behind to enable data binding.

## External Subscription
REs
```
public class MakeReservationCommand : AsyncCommandBase	{
	_makeReservationViewModel.PropertyChanged += OnViewModelPropertyChanged;
}

private void OnViewModelPropertyChanged(object sender, PropertyChangedEventArgs e)	{
    if(e.PropertyName == nameof(MakeReservationViewModel.Username))
    {
	OnCanExecutedChanged();
    }
}
```
1. In the code above, `PropertyChanged` is an event in `MakeReservationCommand` class which gets invoked every time `RaisePropertyChanged` is called
2. `PropertyChanged` on invking passes class name where it is invoked from and the property name it gets invoked from as given : `PropertyChanged?.Invoke(this, new PropertyChangedEventArgs(propertyName));`
3. So `OnViewModelPropertyChanged` checks if the property name being invoked from `Username` property

```
 public string Username {
     get  { return _username; }

     set  {
         _username = value;
         OnPropertyChanged(nameof(Username));

         if(!HasUsername)  {
             AddError("Username cannot be empty.", nameof(Username));
         }
     }
 }
```

# Syncfusion

## Syncfusion List
xaml code
```
<Window x:Class="YourNamespace.MainWindow"  
        xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"  
        xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"  
        xmlns:syncfusion="http://schemas.syncfusion.com/wpf"  
        Title="SfDataGrid Example" Height="350" Width="525">  
    <Grid>  
        <syncfusion:SfDataGrid AutoGenerateColumns="False" ItemsSource="{Binding YourData}">  
            <syncfusion:SfDataGrid.Columns>  
                <syncfusion:GridTextColumn Header="TextBlock" MappingName="TextBlock" />  
                <syncfusion:GridTemplateColumn Header="TextBox">  
                    <syncfusion:GridTemplateColumn.CellTemplate>  
                        <DataTemplate>  
                            <TextBox Text="{Binding TextBox, UpdateSourceTrigger=PropertyChanged}" Width="100"/>  
                        </DataTemplate>  
                    </syncfusion:GridTemplateColumn.CellTemplate>  
                </syncfusion:GridTemplateColumn>  
            </syncfusion:SfDataGrid.Columns>  
        </syncfusion:SfDataGrid>  
    </Grid>  
</Window>
```
`<syncfusion:GridTemplateColumn.CellTemplate>` is set for the particular column when you want to have a disctinctive property of the colum apart from the text.


Code behind
```
using System.Collections.ObjectModel;  
using System.Windows;  

namespace YourNamespace  
{  
    public partial class MainWindow : Window  
    {  
        public ObservableCollection<Item> YourData { get; set; }  

        public MainWindow()  
        {  
            InitializeComponent();  
            YourData = new ObservableCollection<Item>();  
            for (int i = 1; i <= 13; i++)  
            {  
                YourData.Add(new Item { TextBlock = $"Item {i}", TextBox = $"Text {i}" });  
            }  
            DataContext = this;  
        }  
    }  

    public class Item  
    {  
        public string TextBlock { get; set; }  
        public string TextBox { get; set; }  
    }  
}
```
## Working with Syncfusion Chart

XAML file
```
<Window x:Class="WpfApp.MainWindow"  
        xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"  
        xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"  
        xmlns:syncfusion="http://schemas.syncfusion.com/wpf"  
        Title="Syncfusion Chart Example" Height="450" Width="800">  
    
    <Grid>  
        <syncfusion:SfChart Title="Sample Chart">  
            <syncfusion:SfChart.PrimaryAxis>  
                <syncfusion:NumericalAxis Title="X Axis" />  
            </syncfusion:SfChart.PrimaryAxis>  

            <syncfusion:SfChart.SecondaryAxis>  
                <syncfusion:NumericalAxis Title="Y Axis" />  
            </syncfusion:SfChart.SecondaryAxis>  

            <syncfusion:LineSeries ItemsSource="{Binding Data}"   
                                   XBindingPath="XValue"   
                                   YBindingPath="YValue"   
                                   StrokeThickness="2"   
                                   Title="Line Series" />  
        </syncfusion:SfChart>  
    </Grid>  
</Window>
```

ViewModel File<br>
```
using System.Windows;  

namespace WpfApp  
{  
    public partial class MainWindow : Window  
    {  
        public MainWindow()  
        {  
            InitializeComponent();  
            DataContext = new MainViewModel();  
        }  
    }  
}
```
DataModel
```
public class ChartData  
{  
    public double XValue { get; set; }  
    public double YValue { get; set; }  
}
```
Injecting Data
```
using System.Collections.ObjectModel;  

public class MainViewModel  
{  
    public ObservableCollection<ChartData> Data { get; set; }  

    public MainViewModel()  
    {  
        Data = new ObservableCollection<ChartData>  
        {  
            new ChartData { XValue = 1, YValue = 23 },  
            new ChartData { XValue = 2, YValue = 45 },  
            new ChartData { XValue = 3, YValue = 56 },  
            new ChartData { XValue = 4, YValue = 34 },  
            new ChartData { XValue = 5, YValue = 78 },  
            new ChartData { XValue = 6, YValue = 12 },  
            new ChartData { XValue = 7, YValue = 90 }  
        };  
    }  
}
```
## SfDataGrid.Columns
To display employee list on the data grid by pushing the list directly to the grid:
```
HeaderText="Incidence" MappingName="IncidenceType"
```
This is only meant for naming the columns correctly else it doesn't limit the number of columns even if you delete this line
```
using System.Collections.ObjectModel;  
using System.ComponentModel;  

namespace YourNamespace  
{  
    public class Employee  
    {  
        public int Id { get; set; }  
        public string Name { get; set; }  
        public int Age { get; set; }  
        public string Department { get; set; }  
    }  

    public class MainViewModel : INotifyPropertyChanged  
    {  
        public ObservableCollection<Employee> EmployeeList { get; set; }  

        public MainViewModel()  
        {  
            EmployeeList = new ObservableCollection<Employee>  
            {  
                new Employee { Id = 1, Name = "John Doe", Age = 30, Department = "HR" },  
                new Employee { Id = 2, Name = "Jane Smith", Age = 25, Department = "IT" },  
                new Employee { Id = 3, Name = "Emily Johnson", Age = 35, Department = "Finance" },  
                new Employee { Id = 4, Name = "Michael Brown", Age = 40, Department = "Marketing" }  
            };  
        }  

        public event PropertyChangedEventHandler PropertyChanged;  

        protected void OnPropertyChanged(string propertyName)  
        {  
            PropertyChanged?.Invoke(this, new PropertyChangedEventArgs(propertyName));  
        }  
    }  
}
```

xaml code 
```
<Window x:Class="YourNamespace.MainWindow"  
        xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"  
        xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"  
        xmlns:syncfusion="http://schemas.syncfusion.com/wpf"  
        Title="SfDataGrid Example" Height="450" Width="800">  
    <Grid>  
        <syncfusion:SfDataGrid x:Name="dataGrid"  
                                ItemsSource="{Binding EmployeeList}">  
            <syncfusion:SfDataGrid.Columns>  
                <syncfusion:GridTextColumn MappingName="Id" HeaderText="Employee ID" Width="100"/>  
                <syncfusion:GridTextColumn MappingName="Name" HeaderText="Employee Name" Width="200"/>  
                <syncfusion:GridNumericColumn MappingName="Age" HeaderText="Age" Width="100"/>  
                <syncfusion:GridTextColumn MappingName="Department" HeaderText="Department" Width="150"/>  
            </syncfusion:SfDataGrid.Columns>  
        </syncfusion:SfDataGrid>  
    </Grid>  
</Window>
```
# Keywords
## Difference between * and auto
`*` <br>
Meaning: The star size is a proportional sizing method used in layouts, usually found in Grid containers. When you set a dimension (height or width) to *, it indicates that the space should be allocated based on a proportion of the available space in the parent container. <br>

`auto` <br>
Meaning: When you set a dimension to Auto, it tells the layout to size the element based on its content. This means the width or height of the element will be just enough to fit its content without any extra space.


## `UpdateTriggerSouce=PropertyChanged`
this continously calls the property update on each new number press

## IValueConverter
1. IValueConverter is an interface that allows you to define a way to convert data from one type to another for use in user interfaces.
2. You will need to implement the IValueConverter interface, which requires you to define two methods: Convert and ConvertBack

```
using System;  
using System.Globalization;  
using System.Windows;  
using System.Windows.Data;  

public class BooleanToVisibilityConverter : IValueConverter  
{  
    // Converts a Boolean value to Visibility  
    public object Convert(object value, Type targetType, object parameter, CultureInfo culture)  
    {  
        if (value is bool boolValue)  
        {  
            return boolValue ? Visibility.Visible : Visibility.Collapsed;  
        }  
        return Visibility.Collapsed; // Default for non-Boolean input  
    }  

    // Converts a Visibility value back to Boolean  
    public object ConvertBack(object value, Type targetType, object parameter, CultureInfo culture)  
    {  
        if (value is Visibility visibilityValue)  
        {  
            return visibilityValue == Visibility.Visible;  
        }  
        return false; // Default for non-Visibility input  
    }  
}
```
```
<Window x:Class="YourNamespace.MainWindow"  
        xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"  
        xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"  
        xmlns:local="clr-namespace:YourNamespace"  
        Title="MainWindow" Height="350" Width="525">  
    <Window.Resources>  
        <local:BooleanToVisibilityConverter x:Key="BooleanToVisibilityConverter" />  
    </Window.Resources>  
    
    <Grid>  
        <CheckBox x:Name="MyCheckBox" Content="Show Element" />  
        
        <TextBlock Text="Hello, World!"  
                   Visibility="{Binding IsChecked, ElementName=MyCheckBox, Converter={StaticResource BooleanToVisibilityConverter}}"   
                   Margin="10" />  
    </Grid>  
</Window>
```
# Finding
1. In UI, on loading it first falls in the constructor and then the property call triggers i.e the constructor values are updated first and then the property values as given below(in the set function)
```
private bool _proceedWithDiscard = false;
public bool ProceedWithDiscard
{
    get { return _proceedWithDiscard; }
    set
    {
	if (_proceedWithDiscard != value)
	{
	    _proceedWithDiscard = value;
	    RaisePropertyChanged(nameof(ProceedWithDiscard));
	}
    }
}
```

2. updating private values like `_proceedWithDiscard`  doesn't update update actual property
