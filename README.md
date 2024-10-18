import random
import math
from collections import Counter
import matplotlib.pyplot as plt

def normal_cdf(x,mu,sigma):
    return(1+math.erf((x-mu)/(sigma* math.sqrt(2))))/2

def brenoulli_trail(p):
    return 1 if random.random()<p else 0

def binomail(n,p):
    return sum(brenoulli_trail(p) for _ in range(n))

def make_hist(p,n,num_points):
    data=[binomail(n,p) for _ in range(num_points)]
    histogram=Counter(data)
    plt.bar([x-0.4 for x in histogram.keys()],[v/num_points for v in histogram.values()],0.8,color='0.75')
    mu=p*n
    sigma=math.sqrt(n*p*(1-p))
    xs=range(min(data),max(data)+1)
    ys=[normal_cdf(i+0.5,mu,sigma)-normal_cdf(i-0.5,mu,sigma) for i in xs]
    plt.plot(xs,ys)
    
    plt.title("Binomial Distribution V/S Normal Distribution")
    plt.xlabel("Number of Success")
    plt.ylabel("Probability")
    plt.show()
    
make_hist(0.3,50,100)
