# Chapter 1

The xApp Developer Guide can be found here: [https://cutt.ly/drax-xapp-dev-guide](https://cutt.ly/drax-xapp-dev-guide)

# Chapter 2

## See data from the dRAX RIC Databus

You can check the data from the dRAX RIC Databus by logging it in the xApp. This is shown in Example 1 of the `processor.py`.

```
logging.info("dRAX Databus message: {data}".format(data=data))
```

## Create a new structure based on multiple data messages

We can use the internal data_store dictionary to save data from multiple messages. Check example 2 in `processor.py`:

```
if 'type' in data:

            if data['type'] == 'THROUGHPUT_REPORT':
                data_store.setdefault(data['throughputReport']['ueRicId'], {})
                data_store[data['throughputReport']['ueRicId']]['dlThr'] = data['throughputReport']['dlThroughput']
                data_store[data['throughputReport']['ueRicId']]['ulThr'] = data['throughputReport']['ulThroughput']

            elif data['type'] == 'BLER_REPORT':
                data_store.setdefault(data['blerReport']['ueRicId'], {})
                data_store[data['blerReport']['ueRicId']]['dlBler'] = data['blerReport']['dlBler']
                data_store[data['blerReport']['ueRicId']]['ulBler'] = data['blerReport']['ulBler']

        logging.info(data_store)
```

## Publish the new data on the dRAX RIC Databus

You can check example 3 in the `processor.py`:

```
out_queue.put(data_store)
if 'type' in data:
    if data['type'] == 'MY_TEST_TYPE':
        logging.info("dRAX Databus message: {data}".format(data=data))
```
