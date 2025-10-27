# import requests
# import mysql.connector
# import pandas as pd
import numpy as np
from numpy.testing import assert_array_equal, assert_allclose
print('Hello')

# Library 
# Eigenvalues for a 2x2 matrix
# Ax = kx => k is eigenvalue

# A = [[a1, a2]; [a3, a4]]
# det(A - k *I) = |[[a1 - k, a2];
        #           [a3, a4 - k]]|
# (a1 - k) * (a4 - k) - a2 * a3
# = a1a4 - a1k - a4k + k^2 - a2a3 = 0
# -> k^2 - (a1 + a4)*k + (a1a4 - a2a3) = 0
# -> (a1 + a4) +/- \sqrt{((a1 + a4)^2 - 4*(a1a4 - a2a3))} / 2
#
# k1, k2 -> A - k I


def eigv(arr):
    if arr.ndim != 2:
        raise RuntimeError(f'Array should be 2D')
    if arr.shape[0] != arr.shape[1] and arr.shape[0] != 2:
        raise RuntimeError(f'Array should be 2x2')
        
    a1, a2, a3, a4 = arr.flatten().tolist()
    sqrt_term = np.sqrt((a1 + a4) ** 2 - 4.*(a1*a4 - a2*a3))
    result = [((a1 + a4) - sqrt_term) / 2., ((a1 + a4) + sqrt_term) / 2.]
    return result
   

def _get_eigvecs(arr, eigvals):
    # get eigenvectors for each eigenvalue
    # (a1 - k, a2);
    # (a3, a4 -k)  * [x1, x2] = [0, 0]
    eigvecs = []
    for idx, k in enumerate(eigvals):
        A_minus_lambda = np.array([
            [arr[0, 0] - k, arr[0, 1]],
            [arr[1, 0], arr[1, 1] - k]
        ])
        # (a1 - k) *x1 + a2 x2 = 0
        # a3 * x1 + (a4 - k) * x2 = 0
        # x1 = 1
        # ->
        # a1 -k + a2 x2 = 0
        # a3 + (a4 - k) x2 = 0
        # a1 -k - a3 + (a2 - a4 +k) x2 = 0
        # x2 = -(a1 - k - a3) / (a2 - a4 + k)
        a1, a2, a3, a4 = arr.flatten().tolist()
        if idx == 0:
            x1 = 1
            x2 = -(a1 - k - a3) / (a2 - a4 + k)
        else:
        # (a1 - k) *x1 + a2 x2 = 0
        # a3 * x1 + (a4 - k) * x2 = 0
        # x2 = 1
        # ->
        # x1(a1 -k) + a2 = 0
        # a3 x1 + (a4 - k) = 0
        # x1 (a1 -k - a3) + (a2 - a4 +k = 0
        # x2 = -(a2 - a4 + k) / (a1 - k - a3)
            x2 = 1
            x1 = -(a2 - a4 + k) / (a1 - k - a3)
        eigvec = np.array([x1, x2])
        eigvecs.append(eigvec)
    return eigvecs


def test_eigv_diagonals():
    arr = np.zeros((2, 2))
    np.fill_diagonal(arr, 1.0)
    assert_array_equal(eigv(arr), np.array([1, 1]))

    arr[1, 1] = 10
    assert_array_equal(eigv(arr), np.array([1, 10]))

    arr[1, 1] = -10
    assert_array_equal(eigv(arr), np.array([1, -10]))

    arr[1, 1] = 0
    assert_array_equal(eigv(arr), np.array([0, 1]))
 

def test_eigv(arr, x):
    eigvals = eigv(arr)
    print(eigvals)
    eigvecs = _get_eigvecs(arr, eigvals)
    
    for idx, eig in enumerate(eigvals):
        assert_allclose(eig * eigvecs[idx], arr @ eigvecs[idx])

arr = np.random.rand(2, 2)
x = np.random.rand(2, 1)
# arr = np.zeros((2, 2))
# np.fill_diagonal(arr, 1.0)
# A = [0,1,1,0]
arr = np.array([[0,1],[-1,0]])
test_eigv(arr, x)