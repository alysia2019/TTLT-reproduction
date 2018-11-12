The following two sequences were previously used; however, when calling OneHotEncoder's transform, the first observation would have 3 labels instead of 4, corresponding to the number of basepairs. A work-around solution, oneshotonehot, is now in place.


## One hot encoding of sequences
## define the bases we'll use an convert values to an array.
#encoding to integers

def encoded_matrix(kmer_matrix):
    #Define bases and fit labels to use
    encoded_matrix = []
    bases = ['A','C','T','G']
    label_encoder = LabelEncoder()
    base_encoder = label_encoder.fit(bases)
    for i in range(len(kmer_matrix)):
        encoded_base_seq = base_encoder.transform(kmer_matrix[i])
        print(encoded_base_seq)
        encoded_matrix.append(encoded_base_seq)
    return np.vstack(encoded_matrix)

def onehot_matrix(encoded_matrix):
    onehotmatrix = []
    bases = 4
    #We're going to loop through our kmer matrix and turn
    #Every observation into a one-hot encoded array.
    for i in range(len(encoded_matrix)):
        reshaped_vector = encoded_matrix[i].reshape(-1)
        one_hot_vector = np.eye(bases)[reshaped_vector] 
        #encoded_base_seq = encoded_base_seq.reshape(len(encoded_base_seq),1)
        #onehot_encoded_seq = onehot_encoder.fit_transform(encoded_base_seq)
        onehotmatrix.append(one_hot_vector)
    return onehotmatrix
