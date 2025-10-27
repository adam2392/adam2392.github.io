# You have a number of Ads, each belonging to certain category. For a specific user, 
# we can generate a metric score (e.g. CTR) to quantify the value of each Ads. 
# Suppose the Ads are pre-ranked already within each category, and we want to show 
# the top N Ads with the highest scores to the user.

# Input:
# scores: List[List[Tuple]]  
# N: int

# Output: 
# ads_shown: List

# Example:
# scores = [
#     [(0, 0.9), (1, 0.8)], 
#     [(2, 0.85)]
# ]
# N = 2
# ads_shown = [0, 2]
# scores = [
#     [(2, 0.80)]
#     [(0, 0.9), (1, 0.86)], 
# ]
# N = 2
# ads_shown = [0, 1]
# 
# iterate scores, and add the first ad to a heap
# let X category , each category contains Y ads

import heapq


def top_ads(scores, N):
    heap = []
    
    # maps index of categories to specific ad tuple index
    hashmap = dict()
    
    # O(X) time
    # O(X) space
    for idx in range(len(scores)):
        # (-score, ad-id, index)
        score = [-scores[idx][0][1], scores[idx][0][0], idx]
        hashmap[idx] = 1
        heapq.heappush(heap, score)
        
    idx = 0
    result = []
    # O(N log(X)) time
    while heap and idx < N:
        ad_summ = heapq.heappop(heap)
        ad_id = ad_summ[1]
        category_idx = ad_summ[2]
        result.append(ad_id)
        
        # get current index and add the next ad if we're not out of bounds
        jdx = hashmap[category_idx]
        if jdx < len(scores[category_idx]):
            score = [
                -scores[category_idx][jdx][1],
                scores[category_idx][jdx][0],
                category_idx
            ]
            hashmap[category_idx] += 1
            heapq.heappush(heap, score)
        idx += 1
    return result
    
scores = [
     [(0, 0.9), (1, 0.8)], 
     [(2, 0.85)]
]
N = 10
ads_shown = [0, 2, 1]


