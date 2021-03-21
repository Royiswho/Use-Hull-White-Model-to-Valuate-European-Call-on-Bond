# Use Hull-White Model to Valuate European Call on Bond
 
### author: Yi Rong
### date: 03/21/21

---

### Problem
In the Hull–White model, <em>a</em> = 0.08 and <em>&sigma;</em> = 0.02 . Calculate the price of a one-year European  call option on 
a zero-coupon bond that will mature in five years when the term structure is flat at 5%, the principal of the bond 
is $100, and the strike price is $70.

### Solution

It is known that <em>a</em> = 0.08, <em>b</em> = 0.05, &sigma; = 0.02, <em>s</em> = 5, <em>T</em> = 1, <em>L</em> = 100, <em>K</em> = 70. So, we can have:

<img src="media/image1.PNg" width = "350" align="center">

With the results above, the European call price should be:

<img src="media/image2.PNg" width = "500" align="center">

The price should be 11.3077 and the code is shown as below:

```{python }
T = 1
s = 5
L = 100
K = 70
a = 0.08
b = 0.05
sigma = 0.02
P0T = np.exp(-b * T)
P0s = np.exp(-b * s)
sigmaP = (sigma / a) * (1 - np.exp(-a * (s - T))) * np.sqrt((1 - np.exp(-2 * a * T)) / (2 * a))
h = (np.log((L * P0s) / (P0T * K))) / sigmaP + sigmaP / 2
C = L * P0s * si.norm.cdf(h, 0.0, 1.0) - K * P0T * si.norm.cdf(h - sigmaP, 0.0, 1.0)
```