## Part 1 Prediction
At σ = 80 the image is almost pure noise, so D(x; σ) should be a blurry, grayish "average" image, just like the average digit on MNIST. I expect the content to be settled around σ = 1 and after that, only fine details change.

## Part 2 Prediction
Down a column (same starting noise, different class), I expect the overall colors, brightness, background and layout to stay similar, while the object changes to match each row's class.

## Part 3 Prediction
As w goes from 1 to 4, images should look more clearly like the class, but less varied and more exaggerated (saturated colors).

## Part 3
1. Class first shows in D(x; σ) at σ ≈ 3.3 (only a rough layout at 8.4) for w = 1 and σ ≈ 8.4 (similar to w = 1 at σ ≈ 3.3) for w = 4.
2. The image barely changes from σ ≈ 0.3 on. Most of the image is already decided by σ ≈ 1.1. After that only fine details sharpen.
3. At low noise, the w = 4 estimates are more saturated and higher contrast, with sharper more stereotypical cat features (like the ears and eyes). They look a bit exaggerated and less natural than w = 1. The overall layout and pose stay the same since both runs start from the same noise.

## Part 4 Prediction
The shifted mean panel has the largest FID and it comes from the mean term (the shift is 1.5 so roughly 1.5^2 is 2.25).

## Part 5 Prediction
I expect the accuracy to be about 10% at w = 0. It will then jump at w = 1 and keep rising until it plateaus around w = 3-4. The FID should be lowest around w = 1-2 then rise at w = 3-4. Images will get exaggerated and less varied, and FID's spread term will punish that. FID_class will probably improve a little at first as the images match their class better but get worse at a higher w for the same reason.

## Part 5 
I would choose w = 1.5 because the accuracy is already around 99% and the FID at w = 1.5 (31.4) is basically unchanged from w = 0–1 (31.2–31.3). Additionally, the FID_class is at its best (107.6). Past w = 2 accuracy stops improving but FID keeps getting worse and the images look a lot more saturated.

Label accuracy only checks if the classifier sees the requested class and ignores realism and variety and saturates near 99% from w = 1.5 on so it can't tell those w apart. An exaggerated cartoon cat would still count.
FID ignores labels so it would score a dog just as well as when you asked for a cat. That's why w = 0 has the best FID with only an 11.5% accuracy. It also punishes the drop in variety that comes with stronger guidance.
FID_class checks realism within the requested class but with only 100 images per class it's noisy and much higher than FID, so only its trend across w means anything.
None of them measure what a person sees directly so the image grids matter as well.

## Part 6 Prediction
Since the network memorized images of each class, even w = 1 may already give a high accuracy so w > 1 helps less than in part 5.

## Part 6
Across the snapshots, FID rises as training goes on (100 images: 75 -> 110, 1,000 images: 94 -> 133) even though the loss falls. The model memorizes its small training set, so its samples become copies of a few images and match CIFAR-10's variety worse.
My prediction was half right. The 100-image model was already at 93% at w = 1 (100% at w = 2), so guidance had little left to add. But the 1,000-image model went from 40% at w = 1 to 86% at w = 4 which is a much bigger jump than in part 5 (95.5% → ~99%). Guidance helps most when the model’s conditional estimate is weak.

## MNIST Prediction
At w = 0 the request is ignored, so accuracy should be about 10%. It should jump at w = 1 and be close to 100% by w = 2–4 since digits are much easier to tell apart than CIFAR-10 classes. FID should be best around w = 1 and get worse at w = 4 as stronger guidance makes digits thicker, bolder and more alike, like the CIFAR sweep in part 5.

## MNIST CFG network
| w | accuracy | FID (1,000 images, classifier features) |
|---|---|---|
| real digits | – | 19.19 |
| 0 | 10.5% | 136.01 |
| 1 | 97.4% | 22.56 |
| 2 | 100% | 91.31 |
| 4 | 100% | 220.49 |

w = 1 is the best as FID close to real digits. Larger w reaches 100% accuracy but digits get thick and uniform, so FID rises steeply. w = 0 is poor because the unconditional mode only trained on 10% of examples,  unlike CIFAR where w = 0 came from a separate unconditional network trained on all the data.

## Full EDM run 
Trained EDM's unconditional network on all 50,000 images for about 1.5 h (0.55M images) before the server stopped.
Loss 1.0 -> 0.22, FID 412 -> 109. Unlike part 6, FID falls. With the full dataset the model learns to make new
images instead of copying. Still far above the pretrained model's 31.2, as expected.