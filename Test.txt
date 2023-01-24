from kafka import KafkaConsumer

from kafka.errors import KafkaError

from kafka import KafkaConsumer

from sasl import Sasl, SaslMechanism

import ssl

# Set up the SSL/TLS context

ssl_context = ssl.create_default_context(cafile='path/to/truststore.pem')

ssl_context.load_cert_chain('path/to/keytab.pem')

# Set up the Kerberos authentication mechanism

sasl_mechanism = SaslMechanism.GSSAPI

sasl_kerberos_service_name = 'kafka'

# Create a Kafka consumer

consumer = KafkaConsumer(

    'your_topic_name',

    bootstrap_servers='your_kafka_broker_host:port',

    security_protocol='SASL_SSL',

    sasl_mechanism=sasl_mechanism,

    sasl_kerberos_service_name=sasl_kerberos_service_name,

    ssl_context=ssl_context,

    group_id='your_consumer_group',

    auto_offset_reset='earliest',

    value_deserializer=lambda m: json.loads(m.decode('ascii')))

# Consume messages from the topic

for message in consumer:

    print(message.value)

# Close the consumer

consumer.close()

