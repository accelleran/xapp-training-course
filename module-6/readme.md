# Chapter 2: Adding and editing a configuration option 

We change the deployment time configruation options through Helm. We can then edit the configuration options via the dRAX Dashboard. 

To use the configruation options in the xapp_core, we use the following syntax:

```python
with settings.lock:
    our_new_config_option = settings.configuration['config']['TEST_CONFIG']
```

The configuration is stored in the settings variable. This variable has a Lock defined to safeguard the information. Using the Lock we can then read the configruation option.

# Chapter 3:

The xApp Configuration JSON Schema is as follows:

```json
{
    "metadata": {
        "name": "AUTO-GENERATED", # DON’T EDIT
        "configName": "GenericConfigName",
        "namespace": "AUTO-GENERATED" # DON’T EDIT
    },
    "description": "xApp Description...",
    "last_modified": "AUTO-GENERATED", # DON’T EDIT
    'config': {
        ‘'API_GATEWAY_URL': ‘10.20.20.20’, # AUTO-GENERATED, DON’T EDIT
        ‘'API_GATEWAY_PORT': ‘31315’, # AUTO-GENERATED, DON’T EDIT
        'REDIS_URL': '10.20.20.20', # AUTO-GENERATED, DON’T EDIT
        'REDIS_PORT': 32000, # AUTO-GENERATED, DON’T EDIT
        ‘DRAX_COMMAND_TOPIC': 'Topic_OPENRAN_COMMANDS.OranController', # AUTO-GENERATED, DON’T EDIT
        ‘NATS_URL’: 'nats://10.20.20.20:31000', # AUTO-GENERATED, DON’T EDIT
        'LOG_LEVEL': 20,  
        'KAFKA_URL': '10.20.20.20', # AUTO-GENERATED, DON’T EDIT
        'KAFKA_PORT': '31090', # AUTO-GENERATED, DON’T EDIT
        'kafka_producer_topic': 'xapp_specific_topic',
        'KAFKA_LISTEN_TOPIC': 'test2, Topic_State',
        'periodic_publish': True, 
        'publish_interval': 1  # in seconds
    },
    "jsonSchemaOptions": {},
    "uiSchemaOptions": {}
}

```

You can edit this this xApp Configuration JSON Schema and use the enpoint from the dRAX API Gateway to edit the configuration of an xApp:

```shell
curl -X POST -H "Content-Type: application/json" -d @/path/to/xapp-config.json http://<Kubernetes IP>:31315/api/xappconfiguration/config/<xApp Name>
```

Replace:
- /path/to/xapp-config.json: with the absolute path to the JSON file with the above contents
- <Kubernetes IP> with the Kubernetes IP of your setup
- <xApp name> with the name of the xApp you are sending the configuration to

NOTE: The xApp needs to be deployed for the configuration to be stored!