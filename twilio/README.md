# Twilio (SMS/Voice)

## Events Stream Webhook setup

1. Install (CLI client)[https://www.twilio.com/docs/twilio-cli/quickstart]
`brew tap twilio/brew && brew install twilio`

2. Login to Twilio Account.
Account ID and Auth token can be found in (Console Dashboard)[https://console.twilio.com/dashboard], set a profile shorthand identifier ex: twilio-account1.
`twilio login`

3. Activate this profile.
`twilio profiles:use twilio-account1`

4. Create the (Sink)[https://www.twilio.com/docs/events/event-streams/sink-resource] (your webhook)
```
twilio api:events:v1:sinks:create \
  --description="BigQuery pipeline" \
  --sink-configuration='{"destination":"https://your-cloudrun-url/twilio-events","method":"POST"}' \
  --sink-type=webhook
```

5. Validate the sink
```
twilio api:events:v1:sinks:validate:create \
  --sid=DGxxxx \
  --test-id=the-test-id-twilio-sends
```

6. Create a Subscription for required (events)[https://www.twilio.com/docs/events/event-types/messaging/outbound-message]
```
twilio api:events:v1:subscriptions:create \
  --description="SMS events to BQ" \
  --sink-sid=DGxxxx \
  --types '{"type":"com.twilio.messaging.message.sent","schemaVersion":1}' \
  --types '{"type":"com.twilio.messaging.message.delivered","schemaVersion":1}' \
  --types '{"type":"com.twilio.messaging.message.failed","schemaVersion":1}' \
  --types '{"type":"com.twilio.messaging.inbound-message.received","schemaVersion":1}'
```