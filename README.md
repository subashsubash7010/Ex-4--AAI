## NAME : SUBASH M
## Reg_No : 212224220109
## EX. NO : 04
## DATE : 23/02/2026
<H1 ALIGN =CENTER> Implementation of Hidden Markov Model</H1>

## Aim: 
Construct a Python code to find the sequence of hidden states by the known sequence of observances using Hidden Markov Model. Consider two hidden states Sunny and Rainy with observable states,happy and sad.

## Algorithm:

Step 1:Define the transition matrix, which specifies the probability of transitioning from  one hidden state to another.<br>
Step 2:Define the emission matrix, which specifies the probability of observing each possible observation given each hidden state.<br>
Step 3:Define the initial probabilities, which specify the probability of starting in each possible hidden state.<br>
Step 4:Define the observed sequence, which is the sequence of observations need to  be analyzed.<br>
Step 5:Initialize the alpha matrix with zeros, where each row represents a time step and each column represents a possible hidden state.<br>
Step 6:Calculate the first row of the alpha matrix by multiplying the initial  probabilities by the emission probabilities for the first observation.<br>
Step 7:Loop through the rest of the observed sequence and calculate the rest of the alpha matrix by multiplying the emission probabilities by the sum of the product of 
       the previous row of the alpha matrix and the corresponding row of the transition matrix.<br>
Step 8:Calculate the probability of the observed sequence by summing the last row of the alpha matrix.<br>
Step 9:Find the most likely sequence of hidden states by selecting the hidden state with the highest probability at each time step based on the alpha matrix.<br>

## Program:
```
import numpy as np

# Define the transition matrix
transition_matrix = np.array([[0.7, 0.3],
                              [0.4, 0.6]])

# Define the emission matrix
emission_matrix = np.array([[0.1, 0.5, 0.4],
                            [0.6, 0.1, 0.3]])

# Define the initial probabilities
initial_probabilities = np.array([0.6, 0.4])

# Define the observed sequence
observed_sequence = np.array([0, 1, 2, 2])

# Initialize alpha matrix
alpha = np.zeros((len(observed_sequence), len(initial_probabilities)))

# First row
alpha[0, :] = initial_probabilities * emission_matrix[:, observed_sequence[0]]

# Forward algorithm
for t in range(1, len(observed_sequence)):
    for j in range(len(initial_probabilities)):
        alpha[t, j] = (
            emission_matrix[j, observed_sequence[t]] *
            np.sum(alpha[t-1, :] * transition_matrix[:, j])
        )

# Probability of observed sequence
probability = np.sum(alpha[-1, :])

print("The probability of the observed sequence is:", probability)

# Most likely states (NOT true Viterbi, just comparison)
most_likely_sequence = []

for t in range(len(observed_sequence)):
    if alpha[t, 0] > alpha[t, 1]:
        most_likely_sequence.append("rainy")
    else:
        most_likely_sequence.append("sunny")

print("Most likely sequence (based on alpha comparison):", most_likely_sequence)
```

## Output:

<img width="1716" height="89" alt="Screenshot 2026-02-23 081338" src="https://github.com/user-attachments/assets/2e3b564a-0663-44c7-b512-e774b96cade9" />


## Result:
Thus Hidden Markov Model is implemented using python.

