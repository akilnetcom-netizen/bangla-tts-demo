# BD TTS Demo — বাংলা টেক্সট টু স্পিচ

বাংলা লেখা → নিজের VITS মডেলের কণ্ঠে অডিও। কোনো সার্ভার লাগে না, মডেল সরাসরি ব্রাউজারে চলে।

## মডেল
- Hugging Face: https://huggingface.co/demoqqq/banglatts-merged-news/tree/main
- `model_fullmeta.onnx` (114 MB, 22050 Hz, sherpa-onnx VITS, single male news voice)
- `tokens_sherpa.txt` (অবশ্যই এটাই ব্যবহার করতে হবে)

## কীভাবে চালাবেন
1. `index.html` ব্রাউজারে খুলুন, অথবা GitHub Pages / Vercel / Netlify-তে হোস্ট করুন।
2. **মডেল লোড করুন** চাপুন — মডেল Hugging Face থেকে লোড হবে।
3. বাংলা লিখুন → **অডিও বানান** → বাজবে, **WAV ডাউনলোড** করা যাবে।

## সেটিংস
noiseScale 0.667, noiseScaleW 0.8, lengthScale = 1 ÷ গতি, 22050 Hz

## কীভাবে কাজ করে
1. বাংলা অক্ষর → `tokens_sherpa.txt` দিয়ে token id
2. BOS (2) + EOS (1) যোগ করে sherpa-onnx AddBlank (Blank=3)
3. `onnxruntime-web` দিয়ে `model_fullmeta.onnx` চালানো: input, input_lengths, scales=[0.667, lengthScale, 0.8]
4. আউটপুট অডিও বাজানো / WAV সেভ
