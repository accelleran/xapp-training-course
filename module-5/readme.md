# Module 5: dRAX COmmands

# Chapter 5.1: Handover command

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

# Chapter 5.2: Sub-band masking command

## Find our Cell Instance ID

You can check the cell isntance IDs from the dRAX RIC Databus or you can check them on the dRAX Dashboard.

## Create the *sub_band_masking_list*

Next we have to create the *sub_band_masking_list*. You can check Example 5 in `processor.py`.

```python
sub_band_masking_list = [
    {'cell': 'Cell_1', 'num_of_bands': '13', 'mask': [True, True, True, True, True, True, True, True, True, True, True, True, True]},
    {'cell': 'Cell_2', 'num_of_bands': '9', 'mask': [True, True, True, True, True, True, True, True, True]}
]
```

NOTE: Depending on the bandwidth of the cell:
- 20 MHz cells have 13 sub-bands
- 10 MHz cells have 9 sub-bands

You can get these details from the dRAX Dashboard by checking the configuration of the cells. Another way is to use the API Gateway and to GET the cells configuration.

## Trigger the sub-band masking

From Example 5 in the `processor.py`:

```python
send_subband_masking_command(settings, sub_band_masking_list)
```

NOTE: Make sure to wrap up the handover command with a control mechanism in the `processor.py` loop, so that it executes onces!

You can check the details of the sub-band masking command, by looking at the `action_taker.py`.