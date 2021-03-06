[Rocket](../Readme.md)/[coreplex](../coreplex.md)/[RISCVPlatform](https://github.com/freechipsproject/rocket-chip/blob/master/src/main/scala/coreplex/RISCVPlatform.scala)
========================
*RISCV SoC Platform*

**********************

## RISCV Platform

### trait CoreplexRISCVPlatform
*Trait for RISCV SoC platform.*

~~~scala
trait CoreplexRISCVPlatform extends CoreplexNetwork {
  val module: CoreplexRISCVPlatformModule
}
~~~

+ **module** `CoreplexRISCVPlatformModule` pointer to the generated module.
+ **debug** `LazyModule(new TLDebugModule())` debug module.
+ **plic** `LazyModule(new TLPLIC(p(PLICKey)))` platform level interrupt controller.
+ **clint** `LazyModule(new CoreplexLocalInterrupter(p(ClintKey)))` local interrupt?
+ **dts** `DTS(bindingTree)` device tree.
+ **dtb** `DTB(dts)` produce binary device tree.
+ **json** `JSON(bindingTree)` ?? Why JSON version of the device tree again?

### trait CoreplexRISCVPlatformBundle
*Bundle trait for the RISCV SoC Platform.*

~~~scala
trait CoreplexRISCVPlatformBundle extends CoreplexNetworkBundle {
  val outer: CoreplexRISCVPlatform
}
~~~

+ **outer** `CoreplexRISCVPlatform` pointer to the LazyModule.
+ **debug** `new ClockedDMIIO().flip` debug port.
+ **rtcToggle** `Bool(INPUT)` rtc tick input.
+ **resetVector** `UInt(INPUT, p(ResetVectorBits))` resert signals for individual cores.
+ **ndreset** `Bool(OUTPUT)` ??
+ **dmactive** `Bool(OUTPUT)` ??

### trait CoreplexRISCVPlatformModule
*Module trait for the RISCV SoC Platform.*

~~~scala
trait CoreplexRISCVPlatformModule extends CoreplexNetworkModule {
  val outer: CoreplexRISCVPlatform
  val io: CoreplexRISCVPlatformBundle
}
~~~~

+ **outer** `CoreplexRISCVPlatform` pointer to the LazyModule.
+ **io** `CoreplexRISCVPlatformkBundle` pointer to the I/O bundle.

Connect debug I/O ports. Synchronise RTC ticks. Generate DTS and JSON.


<br><br><br><p align="right">
<sub>
Last updated: 20/07/2017<br>
[CC BY-NC-SA 4.0](https://creativecommons.org/licenses/by-nc-sa/4.0/), &copy; (2017) [Wei Song](mailto:wsong83@gmail.com)<br>
[Apache 2.0](https://github.com/freechipsproject/rocket-chip/blob/master/LICENSE.SiFive), &copy; (2016-2017) SiFive, Inc<br>
[BSD](https://github.com/freechipsproject/rocket-chip/blob/master/LICENSE.Berkeley), &copy; (2012-2014, 2016) The Regents of the University of California (Regents)
</sub>
</p>
