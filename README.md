# Extraction of Indian Cultural Elements Using RAG

Extraction of Indian flora and fauna from Indian literary texts using Retrieval-Augmented Generation (RAG). For each of six books from Project Gutenberg, one list of flora and one list of fauna was extracted and stored as Python lists. The lists were then examined for their size, for elements that recur across books and for the kinds of error they contain.

**Author:** Aditya Kumar

**Semester:** Monsoon Semester 2026

**Affiliation:** Department of Humanities and Social Sciences, Indian Institute of Technology (Indian School of Mines), Dhanbad

**Project webpage:** https://adityakumar190.github.io/indian-flora-fauna-rag/

## Research question

How reliably can retrieval-augmented generation extract Indian flora and fauna from Indian literary texts, and what kinds of errors does it make?

## Source texts

All six books are from Project Gutenberg.

| Book | Author | Form | Flora | Fauna |
|---|---|---|---|---|
| [Ancient Ballads and Legends of Hindustan](https://www.gutenberg.org/cache/epub/23245/pg23245-images.html) | Toru Dutt | Ballads and poems | 19 | 9 |
| [Glimpses of Bengal](https://www.gutenberg.org/cache/epub/7951/pg7951-images.html) | Rabindranath Tagore | Letters (translated) | 10 | 6 |
| [Tales of Ind, and Other Poems](https://www.gutenberg.org/cache/epub/11096/pg11096-images.html) | T. Ramakrishna Pillai | Poems | 4 | 4 |
| [The Golden Threshold](https://www.gutenberg.org/cache/epub/680/pg680-images.html) | Sarojini Naidu | Poems | 10 | 13 |
| [The Poison Tree](https://www.gutenberg.org/cache/epub/17455/pg17455-images.html) | Bankim Chandra Chatterjee (translated by Miriam S. Knight) | Novel (translated) | 20 | 10 |
| [Sakoontala](https://www.gutenberg.org/cache/epub/12169/pg12169-images.html) | Kalidasa (translated by Monier Monier-Williams) | Drama (translated) | 7 | 5 |

## Repository contents

| File | Description |
|---|---|
| `flora_fauna.py` | Twelve Python lists: the flora and the fauna extracted from each of the six books (117 entries) |
| `index.html` | Project webpage (published with GitHub Pages) |
| `README.md` | This file |

The lists are named `<book>_flora_RAG_extraction` and `<book>_fauna_RAG_extraction`, for example `the_golden_threshold_flora_RAG_extraction`.

## Method

1. **Selection of texts.** Six books of Indian literature were chosen to cover different forms (verse, letters, a novel and a play) and both original and translated English.
2. **Separate sources.** Each book was treated as a separate source, so the entries for one book come only from that book.
3. **Retrieval and generation.** For each book, passages that mention plants and animals were retrieved, and a language model was asked to list the flora and the fauna named in them. The model often added a short note in brackets to an entry.
4. **Storage.** The entries were saved as two Python lists per book in `flora_fauna.py`.
5. **Examination.** The lists were counted and read against the books.

## Main results

The extraction produced 117 entries: 70 flora and 47 fauna.

- **Recurring elements.** Mango, palm, rose, lotus, jasmine, the peepul (Bo tree), the nightingale and the crow are each named in at least two books.
- **Entries that do not belong.** 27 entries (23%) are in the wrong list or are not plants or animals: 9 animals listed as flora, 7 non-plants listed as flora, 7 people or groups listed as fauna and 4 natural or divine entities listed as fauna.
- **Notes.** 42 entries carry a note in brackets, and 16 of these notes say that the item is implied, likely, general, unspecified or metaphorical.
- **Omissions.** In Ancient Ballads, animals such as deer, peacocks, monkeys, tigers, jackals, elephants and cobras are named in the poems but are not in the fauna list.

The lists are a useful first draft, but every entry should be checked against its passage before reuse. Precision and recall were not measured against a manual annotation.

## Usage

Place `flora_fauna.py` in your project folder and import it:

```python
import flora_fauna as ff

lists = {n: v for n, v in vars(ff).items() if n.endswith("_RAG_extraction")}
print(len(lists))                              # 12 lists
print(sum(len(v) for v in lists.values()))     # 117 entries

flora = ff.the_golden_threshold_flora_RAG_extraction
names = [e.split(" (")[0] for e in flora]      # remove the model's notes
print(names[:3])                               # ['Roses', 'Hyacinths', 'Night-wind']
```

## Limitations

- The lists were not compared with a manual annotation, so precision and recall are not reported.
- Problem entries were identified by reading the lists against the books, and a different reader might classify a few entries differently.
- Names are not normalised, so the same plant or animal can appear in several forms.
- Entries are names only, without the passage or page where they occur.
- Three of the books are translations, so some names reflect the translator's choices.
- Six books are a small sample of Indian literature.

## Citation

Kumar, A. (2026). *Extraction of Indian Cultural Elements Using RAG: Indian Flora and Fauna in Indian Literary Texts*. Department of Humanities and Social Sciences, IIT (ISM) Dhanbad.
