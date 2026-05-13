## Overwrite all configurations 

Full ROS configuration overwrite can be performed using Download RPC FileType="3 Vendor Configuration File" with any URL file name (except with ". alter" extension). 

Warning: Provided configuration file(script) must be "smart" enough to apply configuration correctly right after reboot. This is especially important when using uploaded configuration file with Upload RPC, because it only contains values export. Some things that should be added manually: 

delay at beginning, for interfaces to show up; hidden passwords for users; certificates.
