# Module 4: dRAX API Gateway

# Chapter 4.1: Overview of the dRAX API Gateway

The Swagger page of the dRAX API Gateway can be found on the following URL:

```
<kube-ip>:31315/api/v1/docs/
```

# Chapter 4.2: Using the dRAX API Gateway

## Cell configuration via the API Gateway

You can get the configuration of a cell using the following enpoint of the dRAX API Gateway:

```
/cellconfiguration/summary/{CellInstanceId}
```

You can use Example 6 in the `processor.py` to get the configuration of the cell via the API Gateway:

```
### Example 6: How to get the configuration of a cell 
        endpoint = '/cellconfiguration/summary/<cell-instance-id>'

        api_response = requests.get(
            create_api_url(settings, endpoint)
            )

        if api_response.status_code == 200:
            try:                
                logging.info(api_response.json())
            except:
                logging.warning('Failed to load JSON, showing raw content of API response:')
                logging.info(api_response.text)
        else:
            logging.error("Failed to reach the API Gateway!")
```

We have pre-built the *create_api_url* function so that you dont have to worry about about how to create the URL, which port to use, etc.

## Changing the PCI of a cell

You can use Example 10 from the `processor.py`. Make sure to wrap the example 10 with a control logic that will only execute the code onces (as the code is located in the processor loop).