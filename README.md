# nosql_challenge

help from BCS Support 

query = {'geocode.latitude': {'$gte':latitude-degree_search, '$lte':latitude+degree_search}, 
         'geocode.longitude': {'$gte': longitude-degree_search, '$lte': longitude+degree_search}, 
         'RatingValue':5}
sort = [('scores.Hygiene', 1)]
limit = 5

# Create a pipeline that: 
# 1. Matches establishments with a hygiene score of 0
match_query = {'$match':{'scores.hygiene': 0}}
# 2. Groups the matches by Local Authority
group_query = {'$group':{'_id':'LocalAuthority','count': { '$sum': 1 }} }
# 3. Sorts the matches from highest to lowest
sort_values = {'$sort':{'count': -1}}
# Print the number of documents in the result
pipeline = [match_query, group_query, sort_values]
# Print the first 10 results
results = list(establishments.aggregate(pipeline))
pprint(results)
