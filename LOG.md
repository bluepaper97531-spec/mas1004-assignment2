# Log

One entry for each recipe, selection or Track B model you train, newest at
the bottom. The numbers come from `experiments.csv`. "Why" and "what it means"
are in your own words: your agent asks you for them and does not make them up.
End the log with your plan for what to try next.

<!-- The form of an entry:

## <date> <tag> (Track A or B)
- changed: what is different from the run before
- why: your reason
- validation: 0.000 (before: 0.000)
- what it means: what you think the result says
-->

## 2026-11-06 baseline seed 0 (Track A)
- changed: nothing. the starter recipe as it is, all training photos (44,257)
- why: to have a reference score for every later change
- validation: 0.4984
- what it means: the starter recipe gets about half of the photos right (0.4984), well above the 20% of random guessing. Busan (0.375) and Osaka (0.346) are the weakest cities. This is the reference for all later changes.

## 2026-11-06 baseline seed 1 (Track A)
- changed: only the seed (0 -> 1)
- why: to see how much the score moves by chance
- validation: 0.4979 (before: 0.4984)
- what it means: changing only the seed moved the overall score by just 0.0005, but single cities moved by more (Osaka 0.346 vs 0.389, Busan 0.375 vs 0.394). So an overall change under about 0.01 may be luck, and I should look at the per-city scores carefully. Two seeds are too few to measure the random variation reliably.

## 2026-11-06 b1 (Track B)
- changed: Track B starter setup: ResNet18, 224px, 4 epochs, data/starter/train
- why: first valid Track B release, a reference for later Track B changes
- validation: 0.4952 (Track A seed 0: 0.4984)
- what it means: the starter ResNet18 at 224px scores 0.4952, 0.0032 lower than Track A seed 0. This difference is too small to say that either setup is better, and the budgets differ (249,984 vs 176,896 photos), so it is not a perfectly equal comparison. Track B needs a real change (more photos, a bigger image size or another model) to go beyond this.

## 2026-11-06 photo notes (I looked at training photos of all five cities)
Everything here is by eye, not output of code. Percentages are rough guesses.
- clues I saw: the language written on signs and building walls; traditional buildings, clothing and relics; food; ports, fish markets and other scenes that cannot be seen in inland areas.
- visible at 224px: most of the clues are still recognizable.
- photos without a city clue: about half of the photos showed the cityscape and the differences between cities well. About 20% (by eye) were close-ups of leaves or animals such as sparrows and cats. The other 30% (by eye) were near-copies of the same scene from a slightly different angle, which did not seem very useful. Also, apart from regional and cultural clues such as the sea, fish markets and the language on signs, modern city scenes look mostly alike, so even many of the "good" cityscape photos may not show what separates one city from another.
- near-duplicates: the photos are not all of different places or objects; the same object seems to repeat from similar angles about 3 times.
- my hypothesis, written before measuring: removing training photos that carry no linguistic or geographic clue (for example close-ups of leaves or animals) from selection.csv will raise the validation score, because the model then learns from photos that show signs, writing, sea or other regional features instead of memorizing photos that say nothing about the city.
- how I will measure it: one change in track_a/selection.csv, compared with baseline seed 0 (0.4984). A difference under 0.01 may be luck.

## 2026-11-07 drop91 (Track A)
- changed: removed 91 photos from selection.csv (44,257 -> 44,166), picked by eye from the suspects sheets of the Track B model (b1, 0.4952)
- why: when I looked at the training photos of all five cities, about 20% (by eye) were close-ups of leaves or animals that show nothing about the city, and apart from signs, sea or fish markets, modern city scenes look mostly alike. So I removed only the photos that showed no language or geographic clue, and I kept photos with a clue even when the model got them wrong. I expect the model to memorize fewer photos that say nothing about the city, so the validation score should rise.
- validation: TBD (before: 0.4984)
- what it means: TBD

## Plan
- next: drop the photos with no city clue from selection.csv (one change), compare with baseline seed 0 (0.4984)
- then: reduce near-duplicate frames (separate test)
- Track B: try a bigger image size or more photos
- by 11/9: write the reports