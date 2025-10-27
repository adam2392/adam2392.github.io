import numpy as np

i, j, k, l, m = range(3, 8)

a = np.random.rand(i,k)
b = np.random.rand(j,k)

# Implement a function to contract two N-D arrays 'a' and 'b'.
# 'expr' is an Einstein summation expression like "ik,jk->ij". You may assume one common index for simplicity, if you wish.
def contract(expr, a, b):
    # A_ik @ B_jk
    # 'ik'
    A_idx, B_idx = expr.split(',')
    # 'jk', 'ij'
    B_idx, free_idx = B_idx.split('->')
    
    # 'k'
    joint_idx = set(A_idx).intersection(set(B_idx))
    
    result = np.zeros((len(i_range), len(j_range)))
    
    for i in range(i_range):
        for j in range(j_range):
            result[i, j] = a[i, :].dot(b[j, :])
    return result
    
print(contract("ik,jk->ij", a, b))
assert np.allclose(np.einsum("ik,jk", a, b), contract("ik,jk", a, b)