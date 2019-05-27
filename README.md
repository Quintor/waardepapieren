# Waardepapieren

This project provides a full implementation example of how Discipl components can be used to issue and
verify claims. In particular, how municipalities can issue

## Preparation

In order to make everything functional, we need to generate valid certificates for demo NLX environments and
ensure that the validation app can retrieve those.

1. Generate certificates as described [here](https://docs.nlx.io/get-started/create-certificates/), and place the `org.key` and `org.crt` files at `./waardepapieren-service/system-test/certs/` and just `org.crt` at `./clerk-frontend/public/certs/`

## Running

The easiest way to run is using docker-compose:

This will start 3 applications:

- clerk-frontend
- waardepapieren-service, with embedded ephemeral-server
- nlx-mock, which is an nlx-outway that provides access to a mock BRP service

This is done as follows:

1. Set the environment variable CERT_HOST_IP is with an IP (or domain) that the validator app can use to reach
   the clerk-frontend container. Ensure that the validator app runs on the same (wifi) network as the clerk frontend.
2. Run `docker-compose up`

Alternatively, you can use an offline mock, which replicates the NLX environment.

1. Run `docker-compose -f docker-compose-travis.yml up`

# Running validator
The validator app is made with [Expo](https://expo.io/), which is a free and open-source react-native framework for mobile development. to run this on a mobile device, the expo-cli tool is required. to install this, run:
```bash
$npm install -g expo-cli
```
connect to the same network without firewall restrictions (if all else fails, starting an hotspot on your mobile device and connecting to it usually works). In the folder "validator-frontend", issue the command:
```bash
$expo start
```
wait till the program has fully loaded and scan the QR code in the left bottom corner, with the Expo-app for [Android](https://play.google.com/store/apps/details?id=host.exp.exponent) or [IOS](https://itunes.apple.com/us/app/expo-client/).
