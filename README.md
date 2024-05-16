After Pesting the codes into Power BI, make sure you replace your API Key in the code. If you don't know how to get the key, simply log in to https://serpapi.com/ and navigate to the account section where you'll find the key.

Keyword Limit : Maximum 5 Keywords can be passed

      let
        // Define the API endpoint
        apiUrl = "https://serpapi.com/search.json",
    
    
    // Define the parameters
    queryParams = [ engine = "google_trends", q = "Data Analyst,The Developer,Jobs,India,Power BI" , data_type = "GEO_MAP", date = "today 5-y", tz="-330",api_key = "Peste your Key here"],
    
    // Combine the endpoint and parameters
    fullUrl = apiUrl & "?" & Uri.BuildQueryString(queryParams),
    
    // Make the HTTP request
    response = Web.Contents(fullUrl),
    
    // Parse the JSON response
    jsonResponse = Json.Document(response),
    
    // Convert the response to a table
    dataTable = Table.FromRecords({jsonResponse}),
    
    // Extract the relevant data
    comparedBreakdownByRegion = dataTable{0}[compared_breakdown_by_region]
    in
        comparedBreakdownByRegion
    
This code is used to get data based on the date.

Keyword Limit : Maximum 5 Keywords can be passed

    let
        // Define the base URL for the API call
        BaseUrl = "https://serpapi.com/search",
    
    // Define the query parameters with engine, terms, data type, date, and time zone
    QueryParams = [engine = "google_trends", q = "Data Analyst,The Developer,Jobs,India,Power BI",data_type = "TIMESERIES", date = "all", tz = "-330",    api_key = Key],
    
    // Generate the full URL with query parameters
    UrlWithParams = BaseUrl & "?" & Text.Combine(List.Transform(Record.FieldNames(QueryParams), 
        each _ & "=" & Uri.EscapeDataString(Record.Field(QueryParams, _))), "&"),
    
    // Fetch data from the API
    JsonResponse = Json.Document(Web.Contents(UrlWithParams)),
    
    // Extract the "interest_over_time" part from the JSON response
    InterestOverTime = JsonResponse[#"interest_over_time"]
    in
        InterestOverTime
    
Code for past 7 days keywords performance data.

Keyword Limit : Maximum 5 Keywords can be passed

    let
        // Define the base URL for the API call
        BaseUrl = "https://serpapi.com/search",
    
    // Define the query parameters with engine, terms, data type, date, and time zone
    QueryParams = [engine="google_trends",q="Data Analyst,The Developer,Jobs,India,Power BI", data_type = "TIMESERIES",date = "now 7-d",tz = "-330",api_key = "Peste your key here"],
    
    // Generate the full URL with query parameters
    UrlWithParams = BaseUrl & "?" & Text.Combine(List.Transform(Record.FieldNames(QueryParams), 
        each _ & "=" & Uri.EscapeDataString(Record.Field(QueryParams, _))), "&"),
    
    // Fetch data from the API
    JsonResponse = Json.Document(Web.Contents(UrlWithParams)),
    
    // Extract the "interest_over_time" part from the JSON response
    InterestOverTime = JsonResponse[#"interest_over_time"]
    in
        InterestOverTime
        
Code for related keywords where you'll get two categories of data: Rising Keywords and Top Keywords.

Keyword Limit : Maximum 1 Keywords can be passed

    let
        // Define the API endpoint
        apiUrl = "https://serpapi.com/search.json",
    
    // Define the parameters
    queryParams = [engine = "google_trends",q = "The Developer",data_type = "RELATED_TOPICS",api_key = "Peste your Key"],
    
    // Combine the endpoint and parameters to create the full URL
    fullUrl = apiUrl & "?" & Uri.BuildQueryString(queryParams),
    
    // Make the HTTP request and get the response
    response = Web.Contents(fullUrl),
    
    // Parse the JSON response
    jsonResponse = Json.Document(response)
    in
        jsonResponse
