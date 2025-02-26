## Question 1

The correct answer is `select * from myproject.my_nyc_tripdata.ext_green_taxi`. Even if `raw_nyc_tripdata` is called in the query and could be the dataset, the metadata of the yaml files set an env variable that do have the priority on it

## Question 2
The good answer is `pickup_datetime >= CURRENT_DATE - INTERVAL '{{ var("days_back", env_var("DAYS_BACK", "30")) }}' DAY`

## Question 3
The answer is `dbt run --select models/staging/+` as the fct_taxi_monthly_zone_revenue model does not belongs to staging

## Question 4
It is not mandatory to set both of the ENV
so answer are 3), 4), 5)

## Question 5

