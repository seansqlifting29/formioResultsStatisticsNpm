# Formio Statistics and visualizations

Prepare to have your JSON submissions automated for its statistic results and visualizations!

# Getting Started

## Code

```
export function formioStatsCheckbox(formioSubmissions, checkBoxId) {
    var trueCount = 0;                    
    var falseCount = 0;
    for (var key in formioSubmissions) {           
        for (var sub_key in formioSubmissions[key].data) { 
            if (formioSubmissions[key].data[sub_key] === true && sub_key === checkBoxId) {
                trueCount++;
            }
            if (formioSubmissions[key].data[sub_key] === false && sub_key === checkBoxId) {
                falseCount++;
            }
        }
    }
    console.log((((trueCount * 100) / (trueCount + falseCount)).toFixed(2)) + `% of population selected ${checkBoxId}`);
}
```

## How it works
This function is an opensource code inside a repository contains that will serve as a library for formio users to submit their JSON object form submission results, and have them automatically summarized into visualizations.

## Installation

### Install formio-results-statistics: 

Input (npm i formio-results-statistics) into CLI for install.

### Install Node Fetch: 

Input (npm i node-fetch) into CLI for install.

## Submit Results to Receive Statistics 

### Step One: 

Store your JSON submissions into a folder. These results will be JSON objects containing submission results from formio.io. Go to your project that is referencing a folder or directly storing the JSON submission results.

### Step Two: 

Type in import **formioStatsCheckbox** (this is why you will need Node Fetch installed). Then the function will automatically prompt with at the top of the file:

```
import { formioStatsCheckbox as statsCheckbox } from './node_modules/formio-results-statistics/index.js'
```

### Step Three: 

Rename the function based on your form submissions or application, and now recall that new variable defining the opensource code. Inside the parameters of this recall will be **formioResults** (input for formioSubmissions) and **"male"** (input for checkBoxId). This recall will be displayed as the following:

```
statsCheckbox(formioResults, "male");
```

After the recall is executed, the function will take in these parameters and input them into the function. The function will then go through your folder or variable of Results (array of JSON submissions) and will print for you the statistics and visualizations on that particular attribute.

## Contributing

Pull requests are welcome. For major changes, please open an issue first to discuss what you would like to change. Please make sure to update tests as appropriate.

## License

ISC
