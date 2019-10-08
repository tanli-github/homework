# homework
from IPython.core.display import HTML
import jieba

def word_match(words, title):
    ifmatch = True
    keyword_ = ' '.join(jieba.cut(words))
    for word in keyword_.split():
        if word != ' 'and word not in title:
            ifmatch = False
    return ifmatch

query = '苹果 and (芯片 or 高通)'
query_new_parts = []
for part in list(jieba.cut(query)):
    if part == '(' or part == ')':
        query_new_parts.append(part)
    elif part in ('and', 'AND', 'or', 'OR', 'NOT', 'not', ' '):
        query_new_parts.append(part.lower())
    else:
        query_new_parts.append("word_match('{}',title)".format(part))
query_new = ''.join(query_new_parts)

for title in title_list:
    if eval(query_new):
        for part in list(jieba.cut(query)):
            if part not in ('(',')','and', 'AND', 'or', 'OR', 'NOT', 'not', ' '):
                title = title.replace(part, '<span style="color:red">{}</span>'.format(part))
        display(HTML(title))
