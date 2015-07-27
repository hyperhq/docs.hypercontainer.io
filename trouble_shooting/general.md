# Platform Independent FAQ

## Kernel Problems

#### How can I use my own kernel?

 You can specify your own kernel in the [config file](https://docs.hyper.sh/reference/configuration.html), and reference our [kernel configuration](https://github.com/hyperhq/hyperstart/blob/master/build/kernel_config). 

 If you want use a customized kernel, you need disable the `Cbfs` config item, or build a new cbfs rom ([reference our make cbfs code](https://github.com/hyperhq/hyperstart/blob/master/build/make-initrd.sh#L35)), and I will add a document page on build your own kernel/initrd.
