# openHAB-web-radio
Using the [Sonos Binding](https://www.openhab.org/addons/bindings/sonos/) to allow openHAB to function as web radio by playing `.mp3` live streams. If the URI contains `aac` or does not end by `.mp3` you have to add `x-rincon-mp3radio`.

## Items

You have to create for each live stream a `Switch` item. Later a rule will trigger when a `Switch` item changed to `ON` and play an live stream by using its `URI`.

```
Group Webradio "Webradio" <receiver>

Switch Webradio_SWR1_BW "SWR1 BW" (Webradio)
Switch Webradio_SWR1_RP "SWR1 RP" (Webradio)
Switch Webradio_SWR2 "SWR2" (Webradio)
Switch Webradio_SWR3 "SWR3" (Webradio)
Switch Webradio_SWR_Aktuell "SWR Aktuell" (Webradio)
Switch Webradio_DASDING "DASDING" (Webradio)
Switch Webradio_SWR4_BW "SWR4 BW" (Webradio)
Switch Webradio_SWR4_RP "SWR4 RP" (Webradio)
Switch Webradio_Antenne1 "Hitradio antenne 1" (Webradio)

Group Webradio_Antenne1 "Hitradio antenne 1" <receiver> (Webradio)

Switch Webradio_Antenne1_Live "Hitradio antenne 1 Live" (Webradio_Antenne1)
Switch Webradio_Antenne1_80er "Hitradio antenne 1 80er" (Webradio_Antenne1)
Switch Webradio_Antenne1_90er "Hitradio antenne 1 90er" (Webradio_Antenne1)
Switch Webradio_Antenne1_2000er "Hitradio antenne 1 2000er" (Webradio_Antenne1)
Switch Webradio_Antenne1_Top40 "Hitradio antenne 1 Top 40" (Webradio_Antenne1)
Switch Webradio_Antenne1_ClassicRock "Hitradio antenne 1 Classic Rock" (Webradio_Antenne1)
Switch Webradio_Antenne1_ModernRock "Hitradio antenne 1 Modern Rock" (Webradio_Antenne1)
Switch Webradio_Antenne1_SoftNLazy "Hitradio antenne 1 Soft & Lazy" (Webradio_Antenne1)
Switch Webradio_Antenne1_WeihnachtsHits "Hitradio antenne 1 Weihnachts-Hits" (Webradio_Antenne1)
Switch Webradio_Antenne1_SommerHits "Hitradio antenne 1 Sommer-Hits" (Webradio_Antenne1)
Switch Webradio_Antenne1_DeutschPop "Hitradio antenne 1 Deutsch-Pop" (Webradio_Antenne1)
Switch Webradio_Antenne1_PartyKracher "Hitradio antenne 1 Party-Kracher" (Webradio_Antenne1)
Switch Webradio_Antenne1_UnpluggedAcoustic "Hitradio antenne 1 UnpluggedAcoustic" (Webradio_Antenne1)
Switch Webradio_Antenne1_Oldies "Hitradio antenne 1 Oldies" (Webradio_Antenne1)
Switch Webradio_Antenne1_InTheMix "Hitradio antenne 1 In The Mix" (Webradio_Antenne1)
Switch Webradio_Antenne1_Schlager "Hitradio antenne 1 Schlager" (Webradio_Antenne1)

Group Webradio_SWR3 "SWR3" <receiver> (Webradio)

Switch Webradio_SWR3_Live "SWR3 Live" (Webradio_SWR3)
Switch Webradio_SWR3_Lyrix "SWR3 Lyrix" (Webradio_SWR3)
Switch Webradio_SWR3_Rock "SWR3 Rock" (Webradio_SWR3)
Switch Webradio_SWR3_Party "SWR3 Party" (Webradio_SWR3)
Switch Webradio_SWR3_Mottotage "SWR3 Mottotage" (Webradio_SWR3)
Switch Webradio_SWR3_Specials "SWR3 Specials" (Webradio_SWR3)
```

## Rules

Besides the `Switch` items for each live stream one `<playuri_item>` is needed. The `<playuri_item>` is refered to your `Sonos speaker` which uses the [Sonos Binding](https://www.openhab.org/addons/bindings/sonos/) to play a given `URI`. Also you need an `<control_item>` that you can stop playing the live stream.

```
rule "Webradio Hitradio antenne 1 changed to ON"
when
    Item Webradio_Antenne1 changed to ON
then
    <playuri_item>.sendCommand("http://stream.antenne1.de/a1stg/livestream2.mp3?usid=H-M-09-0-0")
end

rule "Webradio Hitradio antenne 1 changed to OFF"
when
    Item Webradio_Antenne1 changed to OFF
then
    <control_item>.sendCommand(PAUSE)
end

rule "Webradio Hitradio antenne 1 Live changed to ON"
when
    Item Webradio_Antenne1_Live changed to ON
then
    <playuri_item>.sendCommand("http://stream.antenne1.de/a1stg/livestream2.mp3?usid=H-M-09-0-0")
end

rule "Webradio Hitradio antenne 1 Live changed to OFF"
when
    Item Webradio_Antenne1_Live changed to OFF
then
    <control_item>.sendCommand(PAUSE)
end

rule "Webradio Hitradio antenne 1 80er changed to ON"
when
    Item Webradio_Antenne1_80er changed to ON
then
    <playuri_item>.sendCommand("http://stream.antenne1.de/80er/livestream2.mp3?usid=H-M-09-0-0")
end

rule "Webradio Hitradio antenne 80er changed to OFF"
when
    Item Webradio_Antenne1_80er changed to OFF
then
    <control_item>.sendCommand(PAUSE)
end

rule "Webradio Hitradio antenne 1 90er changed to ON"
when
    Item Webradio_Antenne1_90er changed to ON
then
    <playuri_item>.sendCommand("http://stream.antenne1.de/90er/livestream2.mp3?usid=H-M-09-0-0")
end

rule "Webradio Hitradio antenne 90er changed to OFF"
when
    Item Webradio_Antenne1_90er changed to OFF
then
    <control_item>.sendCommand(PAUSE)
end

rule "Webradio Hitradio antenne 1 2000er changed to ON"
when
    Item Webradio_Antenne1_2000er changed to ON
then
    <playuri_item>.sendCommand("http://stream.antenne1.de/2000er/livestream2.mp3?usid=H-M-09-0-0")
end

rule "Webradio Hitradio antenne 2000er changed to OFF"
when
    Item Webradio_Antenne1_2000er changed to OFF
then
    <control_item>.sendCommand(PAUSE)
end

rule "Webradio Hitradio antenne 1 Top 40 changed to ON"
when
    Item Webradio_Antenne1_Top40 changed to ON
then
    <playuri_item>.sendCommand("http://stream.antenne1.de/top40/livestream2.mp3?usid=H-M-09-0-0")
end

rule "Webradio Hitradio antenne Top 40 changed to OFF"
when
    Item Webradio_Antenne1_Top40 changed to OFF
then
    <control_item>.sendCommand(PAUSE)
end

rule "Webradio Hitradio antenne 1 Top Classic Rock changed to ON"
when
    Item Webradio_Antenne1_ClassicRock changed to ON
then
    <playuri_item>.sendCommand("http://stream.antenne1.de/rock/livestream2.mp3?usid=H-M-09-0-0")
end

rule "Webradio Hitradio antenne Top Classic Rock changed to OFF"
when
    Item Webradio_Antenne1_ClassicRock changed to OFF
then
    <control_item>.sendCommand(PAUSE)
end

rule "Webradio Hitradio antenne 1 Top Modern Rock changed to ON"
when
    Item Webradio_Antenne1_ModernRock changed to ON
then
    <playuri_item>.sendCommand("http://stream.antenne1.de/modernrock/livestream2.mp3?usid=H-M-09-0-0")
end

rule "Webradio Hitradio antenne Top Modern Rock changed to OFF"
when
    Item Webradio_Antenne1_ModernRock changed to OFF
then
    <control_item>.sendCommand(PAUSE)
end

rule "Webradio Hitradio antenne 1 Top Soft & Lazy changed to ON"
when
    Item Webradio_Antenne1_SoftNLazy changed to ON
then
    <playuri_item>.sendCommand("http://stream.antenne1.de/soft/livestream2.mp3?usid=H-M-09-0-0")
end

rule "Webradio Hitradio antenne Top Soft & Lazy changed to OFF"
when
    Item Webradio_Antenne1_SoftNLazy changed to OFF
then
    <control_item>.sendCommand(PAUSE)
end

rule "Webradio Hitradio antenne 1 Top Weihnachts-Hits changed to ON"
when
    Item Webradio_Antenne1_WeihnachtsHits changed to ON
then
    <playuri_item>.sendCommand("http://stream.antenne1.de/weihnachtshits/livestream2.mp3?usid=H-M-09-0-0")
end

rule "Webradio Hitradio antenne Top Weihnachts-Hits changed to OFF"
when
    Item Webradio_Antenne1_WeihnachtsHits changed to OFF
then
    <control_item>.sendCommand(PAUSE)
end

rule "Webradio Hitradio antenne 1 Top Sommer-Hits changed to ON"
when
    Item Webradio_Antenne1_SommerHits changed to ON
then
    <playuri_item>.sendCommand("http://stream.antenne1.de/sommerhits/livestream2.mp3?usid=H-M-09-0-0")
end

rule "Webradio Hitradio antenne Top Sommer-Hits changed to OFF"
when
    Item Webradio_Antenne1_SommerHits changed to OFF
then
    <control_item>.sendCommand(PAUSE)
end

rule "Webradio Hitradio antenne 1 Top Deutsch-Pop changed to ON"
when
    Item Webradio_Antenne1_DeutschPop changed to ON
then
    <playuri_item>.sendCommand("http://stream.antenne1.de/deutschpop/livestream2.mp3?usid=H-M-09-0-0")
end

rule "Webradio Hitradio antenne Top Deutsch-Pop changed to OFF"
when
    Item Webradio_Antenne1_DeutschPop changed to OFF
then
    <control_item>.sendCommand(PAUSE)
end

rule "Webradio Hitradio antenne 1 Top Party-Kracher changed to ON"
when
    Item Webradio_Antenne1_PartyKracher changed to ON
then
    <playuri_item>.sendCommand("http://stream.antenne1.de/partykracher/livestream2.mp3?usid=H-M-09-0-0")
end

rule "Webradio Hitradio antenne Top Party-Kracher changed to OFF"
when
    Item Webradio_Antenne1_PartyKracher changed to OFF
then
    <control_item>.sendCommand(PAUSE)
end

rule "Webradio Hitradio antenne 1 Top Unplugged Accoustic changed to ON"
when
    Item Webradio_Antenne1_UnpluggedAccoustic changed to ON
then
    <playuri_item>.sendCommand("http://stream.antenne1.de/unplugged/livestream2.mp3?usid=H-M-09-0-0")
end

rule "Webradio Hitradio antenne Top Unplugged Accoustic changed to OFF"
when
    Item Webradio_Antenne1_UnpluggedAccoustic changed to OFF
then
    <control_item>.sendCommand(PAUSE)
end

rule "Webradio Hitradio antenne 1 Top Oldies changed to ON"
when
    Item Webradio_Antenne1_Oldies changed to ON
then
    <playuri_item>.sendCommand("http://stream.antenne1.de/oldies/livestream2.mp3?usid=H-M-09-0-0")
end

rule "Webradio Hitradio antenne Top Oldies changed to OFF"
when
    Item Webradio_Antenne1_Oldies changed to OFF
then
    <control_item>.sendCommand(PAUSE)
end

rule "Webradio Hitradio antenne 1 Top In The Mix changed to ON"
when
    Item Webradio_Antenne1_InTheMix changed to ON
then
    <playuri_item>.sendCommand("http://stream.antenne1.de/inthemix/livestream2.mp3?usid=H-M-09-0-0")
end

rule "Webradio Hitradio antenne Top In The Mix changed to OFF"
when
    Item Webradio_Antenne1_InTheMix changed to OFF
then
    <control_item>.sendCommand(PAUSE)
end

rule "Webradio Hitradio antenne 1 Top Schlager changed to ON"
when
    Item Webradio_Antenne1_Schlager changed to ON
then
    <playuri_item>.sendCommand("http://stream.antenne1.de/schlager/livestream2.mp3?usid=H-M-09-0-0")
end

rule "Webradio Hitradio antenne Top Schlager changed to OFF"
when
    Item Webradio_Antenne1_Schlager changed to OFF
then
    <control_item>.sendCommand(PAUSE)
end

rule "Webradio SWR1 BW changed to ON"
when
    Item Webradio_SWR1_BW changed to ON
then
    <playuri_item>.sendCommand("https://d131.rndfnk.com/ard/swr/swr1/bw/mp3/128/stream.mp3?aggregator=web&cid=01FC1X3K2Z71SMDKMEC68DM7MW&sid=2D9g9Jx51DuDZCf3L3y7b3BiHwQ&token=k_FTXGAGjgcQvgGM8KfOsmFtC8X1JI-LUYNnFUMna0I&tvf=tIGCxNz-CRdkMTMxLnJuZGZuay5jb20")
end

rule "Webradio SWR1 BW changed to OFF"
when
    Item Webradio_SWR1_BW changed to OFF
then
    <control_item>.sendCommand(PAUSE)
end

rule "Webradio SWR1 RP changed to ON"
when
    Item Webradio_SWR1_RP changed to ON
then
    <playuri_item>.sendCommand("https://f111.rndfnk.com/ard/swr/swr1/rp/mp3/128/stream.mp3?aggregator=web&cid=01FC1X3Q82Y5KQ31V7YJVJJ07W&sid=2D9gUDldYx4rOlV7ycvKlgwIncZ&token=FWfMBjq_y0Tz7xNa88jSJpJFZbmw5PSh1CIu8DjgzPk&tvf=40H_bwP_CRdmMTExLnJuZGZuay5jb20")
end

rule "Webradio SWR1 RP changed to OFF"
when
    Item Webradio_SWR1_RP changed to OFF
then
    <control_item>.sendCommand(PAUSE)
end

rule "Webradio SWR2 changed to ON"
when
    Item Webradio_SWR2 changed to ON
then
    <playuri_item>.sendCommand("https://d131.rndfnk.com/ard/swr/swr2/live/mp3/256/stream.mp3?aggregator=web&cid=01FC1X4J91VJW1CVH6588MZEE3&sid=2D9gbkxIZPCONkbgNsF1JSsPTfq&token=WjX9HlSm5tKRLZOBAI2ZAMOMHZ73mbrVHKM3guPlzn0&tvf=myxZXRH_CRdkMTMxLnJuZGZuay5jb20")
end

rule "Webradio SWR2 changed to OFF"
when
    Item Webradio_SWR2 changed to OFF
then
    <control_item>.sendCommand(PAUSE)
end

rule "Webradio SWR3 changed to ON"
when
    Item Webradio_SWR3 changed to ON
then
    <playuri_item>.sendCommand("https://d121.rndfnk.com/ard/swr/swr3/live/mp3/128/stream.mp3?aggregator=web&cid=01FC1X5J7PN2N3YQPZYT8YDM9M&sid=2D9gfBju8QbeDa0gfuafFLgMDhk&token=fP3ORreQOqCrnJjY36dldQse5lYtgarP3gVoRlvcAHU&tvf=wqO5qBf_CRdkMTIxLnJuZGZuay5jb20")
end

rule "Webradio SWR3 changed to OFF"
when
    Item Webradio_SWR3 changed to OFF
then
    <control_item>.sendCommand(PAUSE)
end

rule "Webradio SWR Aktuell changed to ON"
when
    Item Webradio_SWR_Aktuell changed to ON
then
    <playuri_item>.sendCommand("https://d121.rndfnk.com/ard/swr/swraktuell/live/mp3/128/stream.mp3?aggregator=web&cid=01FC1X68PSW211RY56CDZQEEEN&sid=2D9gio7RTx4O2hROsDfuEG5MRT1&token=Lk-mn_cvfvuC7jlaFTGeswYchJFLSyrgtV5ZWUcz4QQ&tvf=p-uJRB7_CRdkMTIxLnJuZGZuay5jb20")
end

rule "Webradio SWR Aktuell changed to OFF"
when
    Item Webradio_SWR_Aktuell changed to OFF
then
    <control_item>.sendCommand(PAUSE)
end

rule "Webradio DASDING changed to ON"
when
    Item Webradio_DASDING changed to ON
then
    <playuri_item>.sendCommand("https://f141.rndfnk.com/ard/swr/dasding/live/mp3/128/stream.mp3?aggregator=web&cid=01FBVQWZT2B1KGPFJ7TDHQ1Y2B&sid=2D9glq9pLGPdixItc8XSQx2XIaW&token=wzVN2Bn8BX4tVTafk4I9LF65avwOf7vLOO4RiVGgBVY&tvf=Eyyv4iP_CRdmMTQxLnJuZGZuay5jb20")
end

rule "Webradio DASDING changed to OFF"
when
    Item Webradio_DASDING changed to OFF
then
    <control_item>.sendCommand(PAUSE)
end

rule "Webradio SWR4 BW changed to ON"
when
    Item Webradio_SWR4_BW changed to ON
then
    <playuri_item>.sendCommand("https://f111.rndfnk.com/ard/swr/swr4/bw/mp3/128/stream.mp3?aggregator=web&cid=01FC1X86VT36Q01G4NBJ3Q4R1Z&sid=2D9gptklQZ1pfbwJELHsqAJFfcl&token=nn2-VBTumDScaj-shgLiMw3H0PugYRvJuAOShR3qBYM&tvf=T-IIniv_CRdmMTExLnJuZGZuay5jb20")
end

rule "Webradio SWR4 BW changed to OFF"
when
    Item Webradio_SWR4_BW changed to OFF
then
    <control_item>.sendCommand(PAUSE)
end

rule "Webradio SWR4 RP changed to ON"
when
    Item Webradio_SWR4_RP changed to ON
then
    <playuri_item>.sendCommand("https://f131.rndfnk.com/ard/swr/swr4/rp/mp3/128/stream.mp3?aggregator=web&cid=01FC1XCV71QFMQD2RNKF4BC5HG&sid=2D9gsbtnfcAb1UHhBHqAG3wlYvK&token=n91pcPHq14yLfEC9hQlTcD7-utPHSLAjBWaMXGSAK7o&tvf=1El-hjD_CRdmMTMxLnJuZGZuay5jb20")
end

rule "Webradio SWR4 RP changed to OFF"
when
    Item Webradio_SWR4_RP changed to OFF
then
    <control_item>.sendCommand(PAUSE)
end
```

## Sitemaps

At least you have to add following to your sitemap:

```
Text label="Webradio" icon="receiver" {
    Switch item=Webradio_SWR1_BW label="SWR1 BW"
    Switch item=Webradio_SWR1_RP label="SWR1 RP"
    Switch item=Webradio_SWR2 label="SWR2"
    Switch item=Webradio_SWR3 label="SWR3"
    Switch item=Webradio_SWR_Aktuell label="SWR Aktuell"
    Switch item=Webradio_DASDING label="DASDING"
    Switch item=Webradio_SWR4_BW label="SWR4 BW"
    Switch item=Webradio_SWR4_RP label="SWR4 RP"
    Switch item=Webradio_Antenne1 label="Hitradio antenne 1"
    Text label="Hitradio antenne 1" icon="receiver" {
        Switch item=Webradio_Antenne1_Live label="Hitradio antenne 1 Live"
        Switch item=Webradio_Antenne1_80er label="Hitradio antenne 1 80er"
        Switch item=Webradio_Antenne1_90er label="Hitradio antenne 1 90er"
        Switch item=Webradio_Antenne1_2000er label="Hitradio antenne 1 2000er"
        Switch item=Webradio_Antenne1_Top40 label="Hitradio antenne 1 Top 40"
        Switch item=Webradio_Antenne1_ClassicRock label="Hitradio antenne 1 Classic Rock"
        Switch item=Webradio_Antenne1_ModernRock label="Hitradio antenne 1 Modern Rock"
        Switch item=Webradio_Antenne1_SoftNLazy label="Hitradio antenne 1 Soft & Lazy"
        Switch item=Webradio_Antenne1_WeihnachtsHits label="Hitradio antenne 1 Weihnachts-Hits"
        Switch item=Webradio_Antenne1_SommerHits label="Hitradio antenne 1 Sommer-Hits"
        Switch item=Webradio_Antenne1_DeutschPop label="Hitradio antenne 1 Deutsch-Pop"
        Switch item=Webradio_Antenne1_PartyKracher label="Hitradio antenne 1 Party-Kracher"
        Switch item=Webradio_Antenne1_UnpluggedAcoustic label="Hitradio antenne 1 UnpluggedAcoustic"
        Switch item=Webradio_Antenne1_Oldies label="Hitradio antenne 1 Oldies"
        Switch item=Webradio_Antenne1_InTheMix label="Hitradio antenne 1 In The Mix"
        Switch item=Webradio_Antenne1_Schlager label="Hitradio antenne 1 Schlager"
    }
    Text label="SWR3" icon="receiver" {
        Switch item=Webradio_SWR3_Live label="SWR3 Live"
        Switch item=Webradio_SWR3_Lyrix label="SWR3 Lyrix"
        Switch item=Webradio_SWR3_Rock label="SWR3 Rock"
        Switch item=Webradio_SWR3_Party label="SWR3 Party"
        Switch item=Webradio_SWR3_Mottotage label="SWR3 Mottotage"
        Switch item=Webradio_SWR3_Specials label="SWR3 Specials"
    }
}
```
