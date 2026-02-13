### EX5 Information Retrieval Using Boolean Model in Python
### DATE: 13.02.2026
### AIM: To implement Information Retrieval Using Boolean Model in Python.
### Description:
<div align = "justify">
The Boolean model in Information Retrieval (IR) is a fundamental model used for searching and retrieving information from a collection of documents. It operates on the principles of set theory and logic, where documents are represented as sets of terms or words, and queries are expressed as Boolean expressions using logical operators such as AND, OR, and NOT.
  
### Procedure:
1. ***Initialize the BooleanRetrieval class:*** The BooleanRetrieval class is defined to manage the indexing and searching of documents.
2. ***Constructor and Index Initialization:*** The class constructor initializes an empty index to store the inverted index mapping terms to documents.
3. ***Indexing Documents:***
    <p> a) The index_document method is responsible for indexing documents.
    <p> b) Tokenize the text content of documents, converting them into lowercase terms.
    <p> c) For each term in the document, it adds an entry in the index, associating the term with the document ID. </p>
4. ***Fetch Web Page Text:***
    <p>a) The fetch_webpage_text method uses the requests library to fetch content from a given URL.
    <p>b) Extract text content from the fetched HTML using BeautifulSoup.
    <p>c) The extracted text is returned for further processing.
5. ***Boolean Search:***
    <p>a) The boolean_search method performs Boolean searches on the indexed documents.
    <p>b) Tokenize the input query and iterates through its terms.
    <p>c) For each term in the query, it retrieves documents containing that term and performs Boolean operations (AND, OR, NOT) based on the query's structure.

### Program:
```
import numpy as np
import pandas as pd

class BooleanRetrieval:
    def __init__(self):
        self.index = {}
        self.documents_matrix = None

    def index_document(self, doc_id, text):
        terms = text.lower().split()
        print("Document -", doc_id, terms)

        for term in terms:
            if term not in self.index:
                self.index[term] = set()
            self.index[term].add(doc_id)

    def create_documents_matrix(self, documents):
        terms = list(self.index.keys())
        num_docs = len(documents)
        num_terms = len(terms)

        self.documents_matrix = np.zeros((num_docs, num_terms), dtype=int)

        for i, (doc_id, text) in enumerate(documents.items()):
            doc_terms = text.lower().split()
            for term in doc_terms:
                if term in terms:
                    term_id = terms.index(term)
                    self.documents_matrix[i][term_id] = 1

    def print_documents_matrix_table(self):
        df = pd.DataFrame(self.documents_matrix, columns=self.index.keys())
        print(df)

    def print_all_terms(self):
        print("All terms in the documents:")
        print(list(self.index.keys()))

    def boolean_search(self, query):
        query = query.lower().split()
        all_docs = set()

        for docs in self.index.values():
            all_docs = all_docs.union(docs)

        result = None
        operator = None

        for word in query:
            if word in ["and", "or", "not"]:
                operator = word
            else:
                docs = self.index.get(word, set())

                if result is None:
                    if operator == "not":
                        result = all_docs - docs
                    else:
                        result = docs
                else:
                    if operator == "and":
                        result = result & docs
                    elif operator == "or":
                        result = result | docs
                    elif operator == "not":
                        result = result - docs

        return result


documents = {
    1: "Python is a programming language",
    2: "Information retrieval deals with finding information",
    3: "Boolean models are used in information retrieval"
}

indexer = BooleanRetrieval()

for doc_id, text in documents.items():
    indexer.index_document(doc_id, text)

indexer.create_documents_matrix(documents)
indexer.print_documents_matrix_table()
indexer.print_all_terms()

query = input("Enter your boolean query: ")
results = indexer.boolean_search(query)

if results:
    print(f"Results for '{query}': {results}")
else:
    print("No results found for the query.")

```

### Output:
<img width="1081" height="281" alt="Screenshot 2026-02-13 161941" src="https://github.com/user-attachments/assets/0aa3380e-29c3-4e28-804b-e188ba5511a0" />
<img width="1068" height="286" alt="Screenshot 2026-02-13 162022" src="https://github.com/user-attachments/assets/31c812f9-6887-40a6-b6db-0c8a6765751e" />
<img width="1123" height="276" alt="Screenshot 2026-02-13 162042" src="https://github.com/user-attachments/assets/e719c05f-b894-4db4-8e0a-4400b2f3ba49" />
<img width="1087" height="274" alt="Screenshot 2026-02-13 162114" src="https://github.com/user-attachments/assets/847a541b-f899-4a4a-b578-e6b1ffc44b1a" />
<img width="1144" height="278" alt="Screenshot 2026-02-13 161913" src="https://github.com/user-attachments/assets/2e7f044b-a077-4d3b-98d4-5855f23bb1c9" />



### Result:
Thus,Information Retrieval Using Boolean Model in Python is successfully verified.
