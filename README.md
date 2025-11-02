H. Kerem Yanik
Assignment 7
Programming for Psychologists

Modifications Made

1) Added a confidence prompt stimulus
Created a TextStim shown after each choice to collect a 1–4 confidence rating:

```python
conf_prompt = TextStim(
    win,
    text="How confident are you? 1 = low   4 = high",
    alignText='center',
    height=0.085
)
```

2) Updated on-screen instructions
Appended one sentence informing participants they will rate confidence from **1 (low)** to **4 (high)** after each choice:

```python
task_instruct_txt = """
...
After your choice, please rate your confidence from 1 (low) to 4 (high) using number keys.
"""
```

3) Inserted confidence collection loop
After recording the left/right response and RT, added a loop that waits for number keys **1–4** (ESC still exits) and stores the rating:

```python
kb.clearEvents()
rating = None
while rating is None:
    conf_prompt.draw()
    win.flip()
    keys = kb.getKeys(['1', '2', '3', '4', 'escape'], waitRelease=False)
    if keys:
        k = keys[0].name
        if k == 'escape':
            win.close(); quit()
        else:
            rating = int(k)
```

4) Saved the confidence value to the output file
Logged the rating as a new column in the trial data:

```python
trials.addData('confidence', rating)
```

5) Changed completion text size
Decreased the completion message size for visibility:

```python
end_text = TextStim(win, text="Task complete! Thank you.", height=0.1)
```
