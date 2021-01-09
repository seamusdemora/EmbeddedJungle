Moisture Sensing for Irrigation

There are numerous types of inexpensive moisture sensors available in the market today. In general, they all attempt to detect differences in the electrical properties of wet soil vs. dry soil.

Two commonly-used methods are:

1. Measure the change is resistance of dry soil vs wet soil
2. Measure the change in the dielectric constant of wet soil vs dry soil

Both methods can accurately sense differences in wet and dry soil, but resistance measurement has a significant issue in that [*electrolytic corrosion*](https://www.corrosionpedia.com/definition/1321/electrolytic-corrosion) can be severe, as shown in [this video](https://www.youtube.com/watch?v=udmJyncDvw0). The same video also shows a sensor that indirectly measures the change in dielectric constant fo the soil. Just as wet soil has lower resistance to the flow of current, it also has a much higher dielectric constant. A higher dielectric constant results in increased capacitance, and this can also be measured by several methods. 

However

Is copper impervious to AC-induced corrosion? [That remains an open question](https://www.copper.org/resources/properties/protection/underground.html), but for this to happen seems to require other contributing causes. [Further reading](https://opac.biblio.polimi.it/sebina/repository/link/oggetti_digitali/fullfiles/PERL-TDDE/TESI_D01302.PDF) indicates AC-induced corrosion has occurred in buried metal pipelines which lie directly below high-voltage power lines,  but the mechanism is unknown. While engineers and scientists work to identify the corrosion mechanisms involved, it seams safe to ignore their effects for a low-voltage AC moisture sensor. 

The approach discussed here is different than those above. The sensor is driven with a pure AC signal (no DC component), and the phase shift is measured using a sophisticated, but inexpensive, phase detector.

For the following R-C circuit, there is a [closed-form solution for the phase shift](https://www.translatorscafe.com/unit-converter/en-US/calculator/series-rc-impedance/):  

𝝫 = arctan (-1/2𝝿fCR)

picture/schematic



