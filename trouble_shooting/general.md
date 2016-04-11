# Platform Independent FAQ

## Kernel Problems

#### How can I use my own kernel?

 You can specify your own kernel in the [config file](http://docs.hypercontainer.io/reference/configuration.html), and reference our [kernel configuration](https://github.com/hyperhq/hyperstart/blob/master/build/kernel_config).

 If you want to use a customized kernel, you need to disable the `Cbfs` config item, or build a new cbfs rom ([reference our make cbfs code](https://github.com/hyperhq/hyperstart/blob/master/build/make-initrd.sh#L35)).
