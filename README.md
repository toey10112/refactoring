# Refactoring
Bhatara PA4 [Covid19-Tracker](https://github.com/OOP2020/pa4-bhatara007)

## 1.In setAll() method in WorldController.java
**Refactor**: This method has too many line so we need to exact method to separate
their work and make it easy to read and shorter code.

**Before refactor:**
```java
public void setAll(){

        //set percentage fill color.
        t1.setStyle("-fx-fill: forestgreen");
        t2.setStyle("-fx-fill: forestgreen");
        t3.setStyle("-fx-fill: forestgreen");
        t4.setStyle("-fx-fill: forestgreen");

        // formatted String of the values for display.
        newCase = String.format("%,d", Integer.parseInt(worldDataToday[2]));
        newDeaths = String.format("%,d", Integer.parseInt(worldDataToday[3]));
        totalCases = String.format("%,d", Integer.parseInt(worldDataToday[4]));
        totalDeaths = String.format("%,d", Integer.parseInt(worldDataToday[5]));

        // set a value of divide attributes.
        divide1 = convertDouble(getWorldDataYesterday[indexOfTotalCaseIndex]);
        divide2 = convertDouble(getWorldDataYesterday[indexOfNewCase]);
        divide3 = convertDouble(getWorldDataYesterday[indexOfNewDeath]);
        divide4 = convertDouble(getWorldDataYesterday[indexOfTotalDeath]);

        //fix a value of divide attributes when it equals zero.
        if (divide1 == 0) divide1 = 1;
        if (divide2 == 0) divide2 = 1;
        if (divide3 == 0) divide3 = 1;
        if (divide4 == 0) divide4 = 1;

        //calculate a percentage different.
        percent1 = (convertDouble(worldDataToday[indexOfTotalCaseIndex]) - convertDouble(getWorldDataYesterday[indexOfTotalCaseIndex])) * 100 / divide1;
        percent2 = (convertDouble(worldDataToday[indexOfNewCase]) - convertDouble(getWorldDataYesterday[indexOfNewCase])) * 100 / divide2;
        percent3 = (convertDouble(worldDataToday[indexOfNewDeath]) - convertDouble(getWorldDataYesterday[indexOfNewDeath])) * 100 / divide3;
        percent4 = (convertDouble(worldDataToday[indexOfTotalDeath]) - convertDouble(getWorldDataYesterday[indexOfTotalDeath])) * 100 / divide4;

        // formatted String of the percentage different value for display.
        diff1 = String.format("( %.2f", percent1);
        diff2 = String.format("( %.2f", percent2);
        diff3 = String.format("( %.2f", percent3);
        diff4 = String.format("( %.2f", percent4);

        if (percent1 > 0) {
            diff1 = String.format("( +%.2f", percent1);
            t1.setStyle("-fx-fill: red");
        }
        if (percent2 > 0) {
            diff2 = String.format("( +%.2f", percent2);
            t2.setStyle("-fx-fill: red");
        }
        if (percent3 > 0) {
            diff3 = String.format("( +%.2f", percent3);
            t3.setStyle("-fx-fill: red");
        }
        if (percent4 > 0) {
            diff4 = String.format("( +%.2f", percent4);
            t4.setStyle("-fx-fill: red");
        }

        //set text for display.
        lb1.setText(totalCases);
        lb2.setText(newCase);
        lb3.setText(totalDeaths);
        lb4.setText(newDeaths);
        text.setText("World");
        date.setText("Date: " + worldDataToday[0]);
        t1.setText(diff1 + "% )");
        t2.setText(diff2 + "% )");
        t3.setText(diff3 + "% )");
        t4.setText(diff4 + "% )");
    }
```

**After refactor:**
```
public void setAll(){

        //set percentage fill color.
        setPercentageGreenColour();


        // formatted String of the values for display.
        setString();

        // set a value of divide attributes.
        //fix a value of divide attributes when it equals zero.
        setDivideValue();

        //calculate a percentage different.
        calculatePercentageDifferent();

        // formatted String of the percentage different value for display.
        formatTextPercentageDifferent();

        //set text for display.
        setTextForDisplay();
    }

    /***
     * set string in percentage different.
     */
    public void formatTextPercentageDifferent() {
        diff1 = String.format("( %.2f", percent1);
        diff2 = String.format("( %.2f", percent2);
        diff3 = String.format("( %.2f", percent3);
        diff4 = String.format("( %.2f", percent4);

        if (percent1 > 0) {
            diff1 = String.format("( +%.2f", percent1);
            t1.setStyle("-fx-fill: red");

        }
        if (percent2 > 0) {
            diff2 = String.format("( +%.2f", percent2);
            t2.setStyle("-fx-fill: red");
        }
        if (percent3 > 0) {
            diff3 = String.format("( +%.2f", percent3);
            t3.setStyle("-fx-fill: red");
        }
        if (percent4 > 0) {
            diff4 = String.format("( +%.2f", percent4);
            t4.setStyle("-fx-fill: red");
        }
    }

    /***
     * set text for show display.
     */
    public void setTextForDisplay() {
        lb1.setText(totalCases);
        lb2.setText(newCase);
        lb3.setText(totalDeaths);
        lb4.setText(newDeaths);
        text.setText("World");
        date.setText("Date: " + worldDataToday[0]);
        t1.setText(diff1 + "% )");
        t2.setText(diff2 + "% )");
        t3.setText(diff3 + "% )");
        t4.setText(diff4 + "% )");
    }

    /***
     * calculate percentage different.
     */
    public void calculatePercentageDifferent() {
        percent1 = (convertDouble(worldDataToday[indexOfTotalCaseIndex]) - convertDouble(getWorldDataYesterday[indexOfTotalCaseIndex])) * 100 / divide1;
        percent2 = (convertDouble(worldDataToday[indexOfNewCase]) - convertDouble(getWorldDataYesterday[indexOfNewCase])) * 100 / divide2;
        percent3 = (convertDouble(worldDataToday[indexOfNewDeath]) - convertDouble(getWorldDataYesterday[indexOfNewDeath])) * 100 / divide3;
        percent4 = (convertDouble(worldDataToday[indexOfTotalDeath]) - convertDouble(getWorldDataYesterday[indexOfTotalDeath])) * 100 / divide4;
    }

    /***
     * set a value of divide attributes.
     */
    public void setDivideValue() {
        // set a value of divide attributes.
        divide1 = convertDouble(getWorldDataYesterday[indexOfTotalCaseIndex]);
        divide2 = convertDouble(getWorldDataYesterday[indexOfNewCase]);
        divide3 = convertDouble(getWorldDataYesterday[indexOfNewDeath]);
        divide4 = convertDouble(getWorldDataYesterday[indexOfTotalDeath]);

        //fix a value of divide attributes when it equals zero.
        if (divide1 == 0) divide1 = 1;
        if (divide2 == 0) divide2 = 1;
        if (divide3 == 0) divide3 = 1;
        if (divide4 == 0) divide4 = 1;
    }

    /***
     * set percentage different color to green(default colour).
     */
    public void setPercentageGreenColour() {
        t1.setStyle("-fx-fill: forestgreen");
        t2.setStyle("-fx-fill: forestgreen");
        t3.setStyle("-fx-fill: forestgreen");
        t4.setStyle("-fx-fill: forestgreen");
    }

    /**
     * Method for set Alert massage when we don't have a today data for display
     */
    public void noUpdateAlert() {
        date.setText("No update data for today.");
        text.setText(cb1.getValue());
        lb1.setText("-");
        lb2.setText("-");
        lb3.setText("-");
        lb4.setText("-");
        t1.setText("");
        t2.setText("");
        t3.setText("");
        t4.setText("");
    }

    /***
     * method for set text (newCase , newDeaths , totalCase and totalDeath)
     */
    public void setString(){
        // formatted String of the values for display.
        newCase = String.format("%,d", convertInt(worldDataToday[2]));
        newDeaths = String.format("%,d", convertInt(worldDataToday[3]));
        totalCases = String.format("%,d", convertInt(worldDataToday[4]));
        totalDeaths = String.format("%,d", convertInt(worldDataToday[5]));

    }
```

## 2.In initialize() and draw method in BarChartController.java 
**Refactor**: In this two methods there are some line that duplicate so I use extact method to refactor it.

This is code that duplicate in two methods


**Before refactor:**

```
    for (int i = 1; i < datee.size(); i++) {
        XYChart.Data<String, Number> data = new XYChart.Data<String, Number>(String.valueOf(datee.get(i)), Integer.parseInt(confirmCase.get(i)));
        series.getData().add(data);
    }


```

**After refactor:**

```
/***
     * Method for draw a BarChart
     */
    public void drawBarChart() {

        for (int i = 1; i < datee.size(); i++) {
            String date = String.valueOf(datee.get(i));
            int confirmNumber = Integer.parseInt(confirmCase.get(i));

            XYChart.Data<String, Number> data = new XYChart.Data<String, Number>(date, confirmNumber);
            series.getData().add(data);
        }
    }

```

## 3.Delete setAlert(String alertText) method in BarChartController.java
**Refactor**: I delete setAlert(String alertText) method because it is dead code.

## 4.In getCountryConfirmCase(String type, String country) method in GraphData.java  
**Refactor**: It hard to read so I use switch case to make it look easy to read.

**Before refactor:**
```

        String url = "https://covid.ourworldindata.org/data/ecdc/new_deaths.csv";

        if (type.equals("Total confirmed cases")) url = "https://covid.ourworldindata.org/data/ecdc/total_cases.csv";
        else if (type.equals("Total deaths")) url = "https://covid.ourworldindata.org/data/ecdc/total_deaths.csv";
        else if (type.equals("New confirmed cases")) url = "https://covid.ourworldindata.org/data/ecdc/new_cases.csv";
    ...
```

**After refactor:**
```
String url = "https://covid.ourworldindata.org/data/ecdc/new_deaths.csv";

        switch (type) {
            case "Total confirmed cases":
                url = "https://covid.ourworldindata.org/data/ecdc/total_cases.csv";
                break;
            case "Total deaths":
                url = "https://covid.ourworldindata.org/data/ecdc/total_deaths.csv";
                break;
            case "New confirmed cases":
                url = "https://covid.ourworldindata.org/data/ecdc/new_cases.csv";
                break;
        }
        ...
```

## 5.In cb2.setOnAction method handle(ActionEvent actionEvent) in BarChartController.java and LineChartController.java
**Refactor**: In if == can use to compatre string so i change it to equals

**Before refactor:**
```
public void handle(ActionEvent actionEvent) {
                for (int i = 0; i < confirmCase.size(); i++) {
                    if (cb2.getValue() == datee.get(i)) {
                        casee = confirmCase.get(i);
                    }
                    lb1.setText(String.format("%s : %,d cases", graphType, Integer.parseInt(casee)));
                }
            }
```

**After refactor:**

```
public void handle(ActionEvent actionEvent) {
                for (int i = 0; i < confirmCase.size(); i++) {
                    if (cb2.getValue().equals(datee.get(i))) {
                        casee = confirmCase.get(i);
                    }
                    lb1.setText(String.format("%s : %,d cases", graphType, Integer.parseInt(casee)));
                }
            }
```














   

