# bosh-hm-forwarder-tile

This is a custom tile release of [bosh-hm-forwarder](https://github.com/cloudfoundry/bosh-hm-forwarder).
It was built using the [tile generator](https://docs.pivotal.io/tiledev/tile-generator.html).

As it is a custom tile, it is *not* officially supported by Pivotal GSS.

It is intended only to simplify the setup of bosh-hm-forwarder and save time, with the additional bonus of showing the deployment in the Ops Manager UI.

It includes the `consul_agent` in order to allow metron to find doppler. It uses BOSH links to pull across the relevant details from the cf deployment.

Note: This will only function out of the box against PCF 1.10 and newer, since that is the first version to expose the necessary consul properties via BOSH links. If you want this to work against older PCF versions you will need to add in the necessary properties manually.

## Setup

Setup is simple, as it is a tile with little pre-configuration needed.

1. Download the .pivotal file from the releases page
2. Upload it to Ops Manager
3. Click the tile and fill in the necessary AZ config page
4. Upload the stemcell if needed
5. Click Apply Changes
6. Check the Status page of the new tile once it is deployed for the IP Address of the hm-forwarder/0 machine
7. Enter that IP Address in the "Metrics IP Address" section in the Director Config of the Ops Manager Director tile
8. Click Apply Changes
9. You're done! If you check your firehose log stream you should be able to find `ValueMetric` lines with `origin:"bosh-hm-forwarder"` present.
