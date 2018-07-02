# Data-Base-Mapping

How do we map multiple data source based on name ?

Problem Statement:

Let us assume the following as part of problem,

1) We have master data system. And they do have unique identifier and an organization(institution or companies etc) name corresponding to it
2) We also have various third party source system which holds name of organization

If we have any organization name in third party system which is already present in master data system then we have to ignore it. But if there is 
organization name which is not present in master system then that company detail need to be extracted from third party system and inserted into master system. Mapping can be done only through name of the organization. Because master system and third party system has different identifier.

This may sound like a simple SQL issue. But the trickery part is, Organization names are not exactly same. For example,

Microsoft could be mentioned as MS corp, Microsoft corp or microsoft. So this is where data science intelligence may help to achieve it.

Following are the step I have followed and also mentioned what are all can be improved in existing solution.

1) Load the data file ( Master data source file, Test file which already has mapping, test file)
2) Descriptive analysis of the data
3) Preprocessing of the data like removing special character, convert all the name into capital or small words,etc
4) Merge Company name of master system and test data
5) TF vectroize and generate matrix
6) Split the vector matrix ( one matrix will have vectors of master company name, another matrix will have vectors of test company system)
7) Calculate similarity between the matrix ( Depends upon size of data this may become tedious). This is where library developed by ING comes handy. Please check there GIT hub. They have developed a customized C++ library which will simplify and make it pore effective. Please verify the license before using it
8) Top match of master data company  will be picked for every company in test data with the similarity score
9) Build a (yes/no) classifier based on actual test data and new mapping we have received ( I have used only similarity score as feature. But there can be more feature can be generated like number of char etc)
10) Evaluate and export the classifier
11) So everytime new third party system comes then perform the step 3 to 8. And perform classification using exported classifier. Based on classification result merge the records
