# Chapter 2

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

You can get these details from the dRAX Dashboard by checking the configuration of the cells. Another way is to us ethe API Gateway and to GET the cells configuration.

## Trigger the sub-band masking

From Example 5 in the `processor.py`:

```python
send_subband_masking_command(settings, sub_band_masking_list)
```

NOTE: Make sure to wrap up the handover command with a control mechanism in the `processor.py` loop, so that it executes onces!

You can check the details of the sub-band masking command, by looking at the `action_taker.py`.