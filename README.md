## Golang-Bears

### Descriptions

Initial API draft of golang-bears, an adapted golang version of python pandas.

### Contributions

Want to help bring pandas to Golang? Fork this repo or open issues and make your suggestions.

### Read CSV

```go
dataFrame := gp.ReadCSV("data/file.csv")
```

### Print first 5 rows

```go
df := gp.ReadCSV("data/file.csv")
fmt.Println(df.Head())
```


### Print last 5 rows

```go
df := gp.ReadCSV("data/file.csv")
fmt.Println(df.Tail())
```

### Select rows

```go
df := gp.ReadCSV("data/file.csv")
fmt.Println(df[10:21])
```

### Compute Max on a column

```go
df := gp.ReadCSV("data/file.csv")
fmt.Println(df.Column("Volume").Max())

// OR

fmt.Println(df.Columns([]string{"Volume","Price"}).Max())

```

### Compute Min on a column

```go
df := gp.ReadCSV("data/file.csv")
fmt.Println(df.Column("Volume").Min())

// OR

fmt.Println(df.Columns([]string{"Volume","Price"}).Min())
```

### Compute Mean on a column

```go
df := gp.ReadCSV("data/file.csv")
fmt.Println(df.Column("Volume").Mean())

// OR

fmt.Println(df.Columns([]string{"Volume","Price"}).Mean())
```

### Create Date range

```go
startDate := "2010-01-22"
endDate := "2010-01-26"
dates := gp.DateRange(startDate,endDate)
```

### Create new DataFrame

```go
startDate := "2010-01-22"
endDate := "2010-01-26"
dates := gp.DateRange(startDate,endDate)

df1 := gp.NewDataFrame(gp.NewDataFrameOptions{Index:dates})
```

### Join DataFrames

```go
startDate := "2010-01-22"
endDate := "2010-01-26"
dates := gp.DateRange(startDate,endDate)

df1 := gp.NewDataFrame(gp.NewDataFrameOptions{Index:dates})

df := gp.ReadCSV("data/file.csv").WithOptions(gp.ReadCSVOptions{
	IndexCol:"Date",
	ParseDates:True,
	UseCols:[]string{"Date","Adj Close"},
	NAValues:[]string{"nan"},
})

df1 = df1.Join(df).WithOptions(gp.JoinOptions{
	How:"Inner",
})

df1 = df1.DropNA()
```

### Rename

```go
df := gp.ReadCSV("data/file.csv")
df = df.Rename().Column("Current name", "New name")

// OR

df = df.Rename().Columns([]string{"Current name", "New name"}, []string{"Current name of anothe col", "New name"})
```

### Slicing

```go
df := gp.ReadCSV("data/file.csv")

df.SliceByRow("2010-01-01","2010-01-31").SliceByCol("Net","Vol")
```