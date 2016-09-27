## whereami

Uses WiFi signals and machine learning (sklearn's RandomForest) to predict where you are. Even works for small distances like 2-10 meters.

Your computer will known whether you are on Couch #1 or Couch #2.

## Cross-platform

Works on OSX, Windows, Linux (tested on Ubuntu/Arch Linux).

The package [access_points](https://github.com/kootenpv/accces_points) was created in the process to allow scanning wifi in a cross platform manner. Using `access_points` at command-line will allow you to scan wifi yourself and get JSON output.
`whereami` builds on top of it.

### Installation

    pip install whereami

### Usage

```bash
# in your bedroom, takes 100 samples
whereami learn bedroom 100

# in your kitchen, takes 100 samples
whereami learn kitchen 100

# cross-validated accuracy on historic data
whereami crossval
# 0.99319

# use in other applications, e.g. by piping the most likely answer:
whereami predict | say
# Computer Voice says: "bedroom"

# probabilities per class
whereami predict_proba
# {"bedroom": 0.99, "kitchen": 0.01}
```

If you want to delete some of the last lines, or the data in general, visit your `$USER/.whereami` folder.

### Accuracy

Generally it should work really well. I've been able to learn using only 7 access points at home (test using `access_points -n`). At organizations you might see 70+.

Distance: anything around ~10 meters or more should get >99% accuracy.

If you're adventurous and you want to learn to distinguish between couch #1 and couch #2 (i.e. 2 meters apart), it is the most robust when you switch locations and train in turn. E.g. 20 in Spot A, then 20 in Spot B then start again with A.
Doing this in 100 in spot A, then 100 in spot B and then immediately using "predict" will yield spot B as an answer. No worries, the effect of this temporal overfitting disappears over time. And, in fact, this is only a real concern for the very short distances.

Height: Surprisingly, vertical difference in location is typically even more distinct than horizontal differences.

### Almost entirely "copied" from:

https://github.com/schollz/find

That project used to be in Python, but is now written in Go. `whereami` is in Python with lessons learned implemented.
