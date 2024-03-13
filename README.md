<h1>Large Scale Data Processing - Project 1</h1>
<h2>Steven Roche, Jason Adhinarta</h2>

<h2>Part 1</h2>
<table>
  <tr>
    <th>k Value</th>
    <th>xS</th>
    <th>Hash Value</th>
    <th>Time Elapsed</th>
    <th>Number Trials</th>
  </tr>
  <tr>
    <td>2</td>
    <td>1914965704this_is_a_bitcoin_block_of_48358800_and_56297171</td>
    <td>00ade52d041c9209bfcb8a4b3e0659cf895c54994390e9ea62e2eb67742e396f</td>
    <td>1s</td>
    <td>10000</td>
  </tr>
  <tr>
    <td>3</td>
    <td>143813292this_is_a_bitcoin_block_of_48358800_and_56297171</td>
    <td>000f27f9e6fa56aeacac0def0b0f338407fb81b0cd850c3367e063071bdbd539</td>
    <td>1s</td>
    <td>20000</td>
  </tr>
  <tr>
    <td>4</td>
    <td>770888629this_is_a_bitcoin_block_of_48358800_and_56297171</td>
    <td>0000d222d64afcee0a05fd9907b3c0bdc78c68237c81824de11e9eb5dc7bc9ab</td>
    <td>4s</td>
    <td>999999</td>
  </tr>
  <tr>
    <td>5</td>
    <td>1667221777this_is_a_bitcoin_block_of_48358800_and_5629717</td>
    <td>000007e13c2eee597992bd7ea58de78636f0e687650f4d5986a9a2ab04c1fbdb</td>
    <td>8s</td>
    <td>9999999</td>
  </tr>
  <tr>
    <td>6</td>
    <td>1353069778this_is_a_bitcoin_block_of_48358800_and_56297171</td>
    <td>0000005e2e71862b03d8f0e37d27be10c1e14df08b9b788c838fdb3055e339a</td>
    <td>60s</td>
    <td>99999999</td>
  </tr>
  <tr>
    <td>7</td>
    <td>1204137210this_is_a_bitcoin_block_of_48358800_and_56297171</td>
    <td>0000000363df021ccfc04e0d365ec03631eb1a341156f8e1e94fddd2b0564f1c</td>
    <td>966s</td>
    <td>300000000</td>
  </tr>
</table>


<h2>Part 2: Configuration for Trial 7 </h2>


<h3> Process for Estimating Number of Trials for Trial 7 </h3>
<p>For k=7, I first began with the number of trials for k=6. This resulted in the nonce not being found, and I noticed that the time took about 5 minutes on GCP to run k=6. I did not mind waiting ~15 minutes to find the nonce for k=7, so I estimated tripe the amount of trials to be 300000000. After I ran this once, I got a nonce that worked. In this case I was not very concerned with the runtime. If I was dealing with a larger value for k, I would have likely repeated the smaller trial size many times or increased the number of trials by a smaller percentage. This is because in real bitcoin mining, you need to be the first person to verify the transaction. And the way our code is structured requires that all trials are attempted. So, it would be more helpful to use a smaller trial size and run many batches, assuming we use the randomized approach.</p>

<h2> Part 3: Linear Search for the Nonce </h2>
I changed the way the nonce value is found by altering the code so that each number from 1 to the number of trials is tried, in linear fashion. This is seen in the code uploaded in this repository. This approach should not be any more or less efficient than the randomized approach. First, no nonce value is attempted twice in either approach, so we do not need to consider the possibility of a repitition of a guess. Also, the correct nonce value has no relation to values nearby it, so any guessed nonce value is equally likely as any other value in a given range. Thus, both approaches simply keep guessing numbers until a correct value is found, or until it is found that none of the values work. If we assume that the correct nonce value is uniformly distributed, then any method of working through a given range without repeating a guess is as efficient as another such method. The correct nonce value is randomly selected from any valid 32-bit integer, so the assumption that the correct nonce values should be uniformly distributed is correct. 
