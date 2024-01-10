# failure-event
systemd failure event publisher

    $ sudo su -
    # dnf -y install s-nail
    # echo 'set v15-compat' >> /etc/s-nail.rc
    # echo 'set mta=smtp://YOUR.MX smtp-auth=none' >> /etc/s-nail.rc
    # # Customize failure-event file, and then:
    # cp failure-event /etc/sysconfig/
    # cp failure-event@.service /etc/systemd/system/
    # systemctl daemon-reload
    # # Test that it works
    # systemctl start failure-event@systemd-logind.service

Once the test passes, integrate failure notifications into your systemd services like this:

    [Unit]
    OnFailure=failure-event@%n.service

Don't forget to systemctl daemon-reload after editing systemd units.  If you're adding failure event publishing to 3rd party systemd units, it's probably best to use unit overrides instead of editing the stock files: systemctl edit THIRD_PARTY_SERVICE.
