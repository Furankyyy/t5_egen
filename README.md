# t5_egen


## Installation


Install py_rouge_zh
```
git clone https://github.com/JialeGuo/py_rouge_zh
cd py-rouge-zh
python setup.py install
```

## Stage 1 experiment
```
python run_summarization.py \
    --model_name_or_path Langboat/mengzi-t5-base \
    --do_train \
    --do_eval \
    --do_predict \
    --train_file PATH_TO_{train_1.json} \
    --validation_file PATH_TO_{val_1.json} \
    --test_file PATH_TO_{test_1.json} \
    --text_column text \
    --summary_column summary \
    --output_dir PATH_TO_RESULT_DIR \
    --overwrite_output_dir \
    --per_device_train_batch_size=4 \
    --per_device_eval_batch_size=4 \
    --predict_with_generate \
    --evaluation_strategy epoch \
    --num_train_epochs=5 \
    --max_source_length=128 \
    --max_target_length=64 \
    --load_best_model_at_end=True \
    --save_strategy epoch
```

跑完后我一般`cd PATH_TO_RESULT_DIR`，然后`cat trainer_state.json`，最上面有`best checkpoint`，用这个checkpoint来跑stage 2


## Stage 2 experiment
```
python run_summarization.py \
    --model_name_or_path Langboat/mengzi-t5-base \
    --do_train \
    --do_eval \
    --do_predict \
    --train_file PATH_TO_{train_2.json} \
    --validation_file PATH_TO_{val_2.json} \
    --test_file PATH_TO_{test_2.json} \
    --text_column text \
    --summary_column summary \
    --output_dir PATH_TO_RESULT_DIR \
    --overwrite_output_dir \
    --per_device_train_batch_size=4 \
    --per_device_eval_batch_size=4 \
    --predict_with_generate \
    --evaluation_strategy epoch \
    --num_train_epochs=5 \
    --max_source_length=128 \
    --max_target_length=64 \
    --load_best_model_at_end=True \
    --save_strategy epoch\
    --resume_from_checkpoint PATH_TO_BEST_CHECKPOINT
```

