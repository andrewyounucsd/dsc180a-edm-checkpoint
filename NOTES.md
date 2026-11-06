## Part 3 Answers
1. Class first shows in D(x; σ) at σ ≈ 3.3 (only a rough layout at 8.4) for w = 1 and σ ≈ 8.4 (similar to w = 1 at σ ≈ 3.3) for w = 4.
2. The image barely changes from σ ≈ 0.3 on. Most of the image is already decided by σ ≈ 1.1. After that only fine details sharpen.
3. At low noise, the w = 4 estimates are more saturated and higher contrast, with sharper more stereotypical cat features (like the ears and eyes). They look a bit exaggerated and less natural than w = 1. The overall layout and pose stay the same since both runs start from the same noise.

## Part 4 Prediction
1. The shifted mean panel has the largest FID and it comes from the mean term (the shift is 1.5 so roughly 1.5^2 is 2.25).

## Part 5 Prediction
1. I expect the accuracy to be about 10% at w = 0. It will then jump at w = 1 and keep rising until it plateaus around w = 3-4. The FID should be lowest around w = 1-2 then rise at w = 3-4. Images will get exaggerated and less varied, and FID's spread term will punish that. FID_class will probably improve a little at first as the images match their class better but get worse at a higher w for the same reason.

## Part 6 Prediction
1. Since the network memorized images of each class, even w = 1 may already give a high accuracy so w > 1 helps less than in part 5.