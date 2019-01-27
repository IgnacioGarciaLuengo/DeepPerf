# DeepPerf

Many software systems provide users with a set of configuration options and different configurations may lead to different runtime performance of the system. It is necessary to understand the performance of a system under a certain configuration, before the system is actually configured and deployed. This helps users make rational decisions in configurations and reduce performance testing cost. As the combination of configurations could be exponential, it is impossible to measure system performance under all possible configurations. A recent popular approach is to measure the system performance with only a limited set of configurations (samples), build a performance prediction model and then use the model to predict the performances of the system of a new configuration. DeepPerf is an end-to-end deep learning based solution that can train a software performance prediction model from a limited number of samples and predict the performance value of software system under a new configuration. 

## Prerequisites

- Python 3.6.x
- Tensorflow (tested with tensorflow 1.10.0, 1.8.0)

## Installation

DeepPerf can be directly executed through source code

1. Download and install Python 3.6.x [here](https://www.python.org/downloads/).

2. Install Tensorflow

    ```$ pip3 install tensorflow==1.10.0```

3. Clone DeepPerf

    ``` $ clone https://github.com/DeepPerf/DeepPerf.git```


## Data

DeepPerf has been evaluated on 11 real-world configurable software systems: 
- Apache
- LLVM
- x264
- BDBC
- BDBJ
- SQL
- Dune
- hipacc
- hsmgp
- javagc
- sac

Six of these systems have only binary configuration options, the other five systems have both binary and numeric configuration options. The data is store in the DeepPerf\Data directory. These software systems were measured and published online by the SPLConqueror team. More information of these systems and how they were measured can be found in [here](http://www.fosd.de/SPLConqueror/).

## Usage

To run DeepPerf, users need to specify the name of the software system they wish to evaluate and then run the script `AutoDeepPerf.py`. The script will then evaluate DeepPerf on the chosen software system with 5 different sample sizes (n, 2n, 3n, 4n, 5n with n being the number of options) and 30 experiments for each sample size. For example, if users want to evaluate the system LLVM, the command line to run DeepPerf will be:

    ```$ python AutoDeepPerf.py LLVM```

When finishing each sample size, the script will output a .csv file that shows the mean prediction error and the margin (95% confidence interval) of that sample size over the 30 experiments. There are 11 software systems that users can evaluate: Apache, LLVM, x264, BDBC, BDBJ, SQL, Dune, hipacc, hsmgp, javagc, sac. 

Alternatively, users can customize the sample size and/or the number of experiments for each sample size by using the optional arguments ```-ss``` and ```-ne```. For example, to set the sample size = 20 and the number of experiments = 10, the corresponding command line is:

    ```$ python AutoDeepPerf.py LLVM -ss 20 --ne 10```

Setting none or one option will result in the other option(s) running with the default setting. The default setting for the number of experiments is 30. The default setting for the sample size is the 5 different sample sizes: n, 2n, 3n, 4n, 5n where n is the number of configuration options.

## Experimental Results

<table>
    <thead>
        <tr>
            <th rowspan="2" >Subject System</th>
            <th rowspan="2" >Sample Size</th>
            <th colspan="2" >DECART</th>
            <th colspan="2" >DeepPerf</th>
        </tr>
        <tr>
            <th scope="col">Mean</th>
            <th scope="col">Margin</th>
            <th scope="col">Mean</th>
            <th scope="col">Margin</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td rowspan=5>Apache</td>
            <td>n</td>
            <td>NA</td>
            <td>NA</td>
            <td>17.87</td>
            <td>1.85</td>
        </tr>
        <tr>
            <td>2n</td>
            <td>15.83</td>
            <td>2.89</td>
            <td>10.24</td>
            <td>1.15</td>
        </tr>
        <tr>
            <td>3n</td>
            <td>11.03</td>
            <td>1.46</td>
            <td>8.25</td>
            <td>0.75</td>
        </tr>
        <tr>
            <td>4n</td>
            <td>9.49</td>
            <td>1.00</td>
            <td>6.97</td>
            <td>0.39</td>
        </tr>
        <tr>
            <td>5n</td>
            <td>7.84</td>
            <td>0.28</td>
            <td>6.29</td>
            <td>0.44</td>
        </tr>
        <tr>
            <td rowspan=5>x264</td>
            <td>n</td>
            <td>17.71</td>
            <td>3.87</td>
            <td>10.43</td>
            <td>2.28</td>
        </tr>
        <tr>
            <td>2n</td>
            <td>9.31</td>
            <td>1.30</td>
            <td>3.61</td>
            <td>0.54</td>
        </tr>
        <tr>
            <td>3n</td>
            <td>6.37</td>
            <td>0.83</td>
            <td>2.13</td>
            <td>0.31</td>
        </tr>
        <tr>
            <td>4n</td>
            <td>4.26</td>
            <td>0.47</td>
            <td>1.49</td>
            <td>0.38</td>
        </tr>
        <tr>
            <td>5n</td>
            <td>2.94</td>
            <td>0.52</td>
            <td>0.87</td>
            <td>0.11</td>
        </tr>

    </tbody>
</table>
   
    


    



