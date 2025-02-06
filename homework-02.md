## Homework 2
To achieve this homework, I use Kestra with GCP
### Q1
To see the size of yellow taxi data for the 2020 december's month, just run the flow for this specific dataset and month and look at the size of the csv on google cloud storage
Answer: 128.3 MB

### Q2
Several way to answer this question. We can notice that in the flow the file is called using :
```variables:
  file: "{{inputs.taxi}}_tripdata_{{inputs.year}}-{{inputs.month}}.csv"
```
So Answer: green_tripdata_2020-04.csv

### Q3&Q4
We can created a subflow to extract a whole year. 

```id: green_parent_subflow
namespace: zoomcamp


tasks:
  - id: parallel
    type: io.kestra.plugin.core.flow.ForEach
    concurrencyLimit: 50
    values: ["01", "02", "03", "04", "05", "06", "07", "08", "09", "10", "11", "12"]
    tasks:
      - id: green_20_subflow
        type: io.kestra.plugin.core.flow.Subflow
        flowId: green_20_subflow
        namespace: zoomcamp
        inputs:
          my_input: "{{ taskrun.value }}"
```

Then we slightly change the begining of the flow that extract load and index the files
```
id: green_20_subflow
namespace: zoomcamp
description: |
  it is a subflow
inputs:
  - id: my_input
    type: STRING
    defaults: kestra

variables:
  file: "green_tripdata_2020-{{ inputs.my_input }}.csv"
```

Finally the total rows could be found in several place, for example in the details of the dataset in BigQuery  \n
Answer Q3: 24,648,499 \n
Answer Q4: 1,734,051

### Q5
I added 2021 on possible selection for the flow, then extract and load march 21 in BQ, then read the details
Answer: 1,925,152
### Q6
As New York can belong to two different timezone, the best choice is to select New York as a timezone so the trigger will depends on the calendar
Answer: Add a timezone property set to America/New_York in the Schedule trigger configuration
