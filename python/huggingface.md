# huggingface

## How to get the path to the cached transformer models:
```
from transformers.file_utils import hf_bucket_url, cached_path
pretrained_model_name = "HooshvareLab/bert-fa-base-uncased"
archive_file = hf_bucket_url(
    pretrained_model_name,
    filename='pytorch_model.bin',
)
resolved_archive_file = cached_path(archive_file)
print(resolved_archive_file)
```

## How to test tokenizer
1. how to create:
load from a saved file:
```commandline
base_model = "m3hrdadfi/wav2vec2-large-xlsr-persian-v3" # a persian language!
m3_tokenizer = Wav2Vec2CTCTokenizer.from_pretrained(base_model)
# export the vocabs:
m3_tokenizer.save_vocabulary("m3_vocabs")
# output: m3_vocabs/vocab.json
```
or from vocabulary:
```commandline
tokenizer = Wav2Vec2CTCTokenizer(
            "path_to_vocab_json", # m3_vocabs/vocab.json!
            bos_token="<s>",
            eos_token="</s>",
            unk_token="<unk>",
            pad_token="<pad>",
            word_delimiter_token="|",
            do_lower_case=False # Not needed for languages like persian!
        )
```

How to tokenize:</br>
Output contains input_ids and attention mask. 
1) input_ids are simply token ids
2) attention masks: is used by the model. Those tokens who are masked, means that they are not be shown to the attention layer.
    1) In this example, all the tokens are 1, which means that they are going to be processed by attention layers.

```commandline
output = tokenizer("سلام من پویا هستم")
# {'input_ids': [18, 28, 7, 29, 4, 29, 30, 4, 33, 32, 38, 7, 4, 31, 18, 9, 29], 'attention_mask': [1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1]}
```

How to convert ids to tokens:
```commandline
tokenizer.convert_ids_to_tokens(output["input_ids"])
# output
['س',
 'ل',
 'ا',
 'م',
 '|',
 'م',
 'ن',
 '|',
 'پ',
 'و',
 'ی',
 'ا',
 '|',
 'ه',
 'س',
 'ت',
 'م']
```
**Note:** The '|' is word delimiter token!