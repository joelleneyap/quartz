---
draft: false
tags:
  - clipping
date: 8/20/24
---

how do tell the world about data you cannot show them?
privacy engineer

### wikimedia foundation (WMF)
* nonproit
* develops open-source software and hosts projects like wikipedia, wikidata, commons, mediawiki, etc
* open access policy
	* release as much data about that massive set of sites we run as possible
	* e.g. revision history, wikistats (total page views per month), API (page views)
* existing privacy methods
	* filtering
	* thresholding
	* bucketing
* lean data diet
	* defined by our privacy policy n data retention guidelines
	* no account required to read or edit
	* no cookies that track a single user across the platform
		* hash device IP address and useragent to get actor signature
	* no saving data forever
		* alm all data is aggregated/anonymized and deleted 90 days after collection
	* => minimized time window

tension between privacy and transparency
* minimize harms of collecting user data
* release more data => better to understand the internet
* stakes r high bc wikipedia is inherently political 

### differential privacy
[[A friendly, non-technical introduction to differential privacy - Ted is writing things]]
* a process takes a database in as input and returns some data as output
* add random noise to the process (magic?)
* DP: output shd b basically the same, if we remove one person the database and re-run the process w magic
* exact same outputs w similar likelihood
* => promise: from the pov of someone looking at this data release, ur contribution to this database will b hidden. high-level trends visible, but no one can infer ur presence or absence in the data (even if ur an outlier)
	* outliers: clamp the domain, use DP to calculate the 90% percentile, and clamp everything to the 90% percentile... art not science, everything above a certain threshold is at that threshold
* magic noise is configurable using a parameter called epsilon, which = privacy budget
	* a worse-case bound on how much info can be gleaned from a data release
	* smaller e --> more noise, vice versa
* nosie is form a pseudorandom generator, so its impossible for DP data to b subect to re-identification attacks
* any post-processing w DP data (modelling, sharing, combining w other data) is covered by these guarantees

### the problem
can we use DP to release pageview counts by both project *and* country?
* use anonymous cookies to generate boolean value on the first 10 unique pages that a user visits
* truncate dataset to only include pageviews from popular pages and where boolean=true
* group by country-proj-page and count
* add noise to the data
* red sections are sensitive, green is public data ![[Screenshot 2023-05-07 at 3.27.54 PM.png]]
	* need to draw v strict delineation between public n private
	* difficult arbitrary thing to choose: performance levels of metrics
		* ran 700 experiments, got final output on diff levels --> into google sheets, filter, and filtered by constraints in error metrics ... then 15 to 20. further testing --> breakdown by geography level
			* is this performing well in areas where we still dont get a lot of traffic (e.g. pacific islands)
		* okay, we have this universe of values for all these parameters... shooting for 6% median relative error (if u take the (abs value of the real count of a place - noisy count of the place) / real count... what is the % off = 6%) i.e. 50% of data has greater than 6% relative mean. what does that actly mean for data quality? 
			* what does that mean further on down the road?
			* balancing FP and FN? u can expect that 50% of this is actly fake (random noise)... dataset doesnt seem credible
* similar approach for historical data (preDP cookie)
	* diff kind of noise
	* larger noise scale
	* weaker privacy guarantee
* 8 years of safer more granular data, representing >1 trillion site itneractions
	* publicly accessible and openly licensed
	* safe for post-processing (currently trying to use it to do country level trend modeling)
* future work
	* individual reading session behavior (A -> B -> C pages)
	* grants and grantees
	* editors and edits
	* search patterns
	* banner impressions and click-throughs![[Screenshot 2023-05-07 at 3.36.28 PM.png]]

### privacy
* vibes: u know it when u feel it
	* cultural thing: maybe more in american sphere
* legal definitions: data stewardship (EU), US (incoherent)
* bits of entropy: how much does a given piece of info identify u?
	* how identifiable r u, just from the traces that ur computer leaves arnd the internet?
* DP: context of a single dataset -- net privacy loss?
* feeling in this DP universe, but the adoption is 0
	* no code AI tools
	* DP is 6 years behind that frm a technical pov / open source library that can do that well pov
	* not translating cutting edge research papers... 