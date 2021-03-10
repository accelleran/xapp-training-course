# Chapter 2

## Find out ueDraxId

Find out the ueDraxId of the UE we want to handover. We can simply enable Example 1 in `processor.py` to log the incomming messages on the dRAX RIC Databus. 

```python
logging.info("dRAX RIC Databus message: {data}".format(data=data))

```

We can look for the UE_MEASUREMENT message, which will tell us the ueDraxId as well as the currently serving cell.

We can check the cells also via the dRAX Dashboard.

## Create the *handover_list* variable

Next, we need to create the *handover_list* variable in the `processor.py`. We can check Example 4.

```python
handover_list = [
     {'ueIdx': 'ueDraxId_to_handover_1', 'targetCell': 'Bt1Cell', 'sourceCell': 'Bt2Cell'},
     {'ueIdx': 'ueDraxId_to_handover_2', 'targetCell': 'Bt2Cell', 'sourceCell': 'Bt1Cell'}
]
```

## Trigger the handover

You can use the pre-built function that abstracts the handover command details:

```python
send_handover_command(settings, handover_list)
```

NOTE: Make sure to wrap up the handover command with a control mechanism in the `processor.py` loop, so that it executes onces!

You can check the details of the handover command, by looking at the `action_taker.py`.

