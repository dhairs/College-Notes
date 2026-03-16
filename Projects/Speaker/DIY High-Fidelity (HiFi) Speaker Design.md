High quality speakers require a variety of good materials and design decisions, ours are outlined below.
****

```mermaid
graph TD
    %% Power Distribution
    PowerIC[Power IC] --> BT[Bluetooth Module]
    PowerIC --> MCU[MCU / DSP]

    BT --> MCU
    MCU --> AmpDAC[Amplifier / DAC]

    AmpDAC --> Cap[Inline Capacitor]
    Cap --> Tweeters[Tweeters]
    
    AmpDAC --> Sub[Subwoofer]
    AmpDAC --> Mid[Midrange Woofer]

    style PowerIC fill:#f9f,stroke:#333,stroke-width:2px
    style AmpDAC fill:#bbf,stroke:#333,stroke-width:2px
```

### [Crossover](https://en.wikipedia.org/wiki/Audio_crossover)

We have the option between a digital DSP, or a passive crossover. Passive crossovers are inherently limited in that they are only able to separate set frequencies without the ability to tune without resoldering and re-spec-ing components. 

For this reason, it makes more sense for us to go with a digital crossover. DSPs can handle frequency separation, given there is a sufficiently powerful MCU running it. 

One concern is that the digital crossover doesn't provide protection to the speakers (primarily the tweeters, who will die if we give them super low frequencies) if there is a logic error or issue with the DSP. To ensure that we can still have a safeguard, we can add a high-pass filter with an inline capacitor to act as a passive safeguard if something does happen upstream.

