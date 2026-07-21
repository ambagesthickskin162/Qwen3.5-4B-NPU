# Qwen3.5-4B NPU
![Alt text](https://github.com/user-attachments/assets/6d297a34-c516-4cb1-be4a-bca471d40fa6)
<br><br>**User**:\<image\>Describe the image.<br><br>
**Answer**: This is a surreal, humorous, and slightly absurd depiction of an astronaut relaxing on the Moon — likely in a fictional or satirical context.

**Key elements:**

- **Astronaut**: A person dressed in a bulky white spacesuit with a gold-tinted visor helmet is reclining casually on what appears to be a makeshift chair or cushion made from a green cooler box (possibly repurposed as seating). Their posture suggests complete relaxation — legs stretched out, one hand holding a green glass bottle.

- **The Bottle**: The astronaut is holding a clear green glass bottle with a label that reads “BrewDog” — a well-known Scottish craft beer brand. This adds to the comedic contrast: enjoying a beer in space? It’s impossible under current physics and regulations, but it fits the whimsical tone.

- **Setting**: The background shows the lunar surface — gray, cratered terrain with no atmosphere or clouds. In the distance, Earth hangs prominently in the blackness of space, dotted with stars. A ladder leans against a structure (perhaps part of a base or rover) on the right side.

- **Tone & Style**: The image blends realism (detailed spacesuit, realistic Moon surface and Earth) with fantasy and humor. It plays on pop culture tropes — astronauts drinking beer in space is often used for comedic effect in movies, cartoons, or memes.

**Interpretation:**
This isn’t a real photograph — it’s digitally manipulated or conceptually imagined art meant to evoke amusement. It juxtaposes the solemnity of space exploration with the trivial pleasure of enjoying a drink, creating irony and levity.

In short: *An astronaut lounging on the Moon, sipping BrewDog beer, with Earth watching over them.* 🌕🍻🌍

------------

## Qwen3.5-4B VLM for RK3588 NPU (Rock 5, Orange Pi 5). <br/>
[![License](https://img.shields.io/badge/License-BSD%203--Clause-blue.svg)](https://opensource.org/licenses/BSD-3-Clause)<br/><br/>
Paper: [Qwen3 Technical Report](https://arxiv.org/pdf/2505.09388)<br/><br/>

------------

## Introduction

LLMs (Large Language Models) are neural networks trained on large text datasets to understand and generate language.<br>
VLMs (Vision-Language Models) add a visual encoder so the model can process images and text together.<br> 
A combined VLM+LLM system is often referred to as a multimodal model.

These models can be large—hundreds of millions to billions of parameters—which impacts accuracy, memory use, and runtime speed.<br>
On edge devices like the RK3588, available RAM and compute are limited, and even the NPU has strict constraints on supported operations.<br>
Because of this, models typically need to be quantised or simplified to fit.

Performance is usually expressed in tokens (words) per second.<br>
Once converted to RKNN, parts of the model can run on the NPU, improving speed.<br>
Despite these limits, models like Qwen3-2B run well on the RK3588 because the NPU efficiently accelerates the heavy math, and the vision encoder can be optimised. This makes advanced multimodal AI feasible on small, power-efficient devices.

------------

## Model performance benchmark (FPS)

All models, with C++ examples, can be found on the Q-engineering GitHub.<br><br>
All LLM models are quantized to **w8a8**, while the VLM vision encoders use **fp16**.<br>

| model         | RAM (GB)<sup>1</sup> | llm cold sec<sup>2</sup> | llm warm sec<sup>3</sup> | vlm cold sec<sup>2</sup> | vlm warm sec<sup>3</sup> | Resolution | Tokens/s |
| --------------| :--: | :-----: | :-----: | :--------: | :-----: | :--------:  | :--------: |
| [Qwen3.5-9B](https://github.com/Qengineering/Qwen3.5-9B-NPU) | 9.2 | 97.1 | 97.1 | 11.5  | 11.5 | 448 x 448 | 3.2 |
| [Qwen3.5-4B](https://github.com/Qengineering/Qwen3.5-4B-NPU) | 5.4 | 52.8 | 6.2 | 8.5  | 0.9 | 448 x 448 | 5.2 |
| [Qwen3.5-2B](https://github.com/Qengineering/Qwen3.5-2B-NPU) | 2.9 | 23.9 | 3.2 | 8.5  | 0.8 | 448 x 448 | 11.0 |
| [Qwen3.5-0.8B](https://github.com/Qengineering/Qwen3.5-0.8B-NPU) | 1.3 | 10.6 | 1.9 | 2.7  | 0.2 | 448 x 448 | 21.6 |
| [Qwen3-2B](https://github.com/Qengineering/Qwen3-VL-2B-NPU) | 3.1 | 21.9 | 2.6 | 10.0  | 0.9 | 448 x 448 | 11.5 |
| [Qwen3-4B](https://github.com/Qengineering/Qwen3-VL-4B-NPU) | 8.7 | 49.6 | 5.6 | 10.6  | 1.1 | 448 x 448 | 5.7 |
| [InternVL3.5-1B](https://github.com/Qengineering/InternVL3.5-1B-NPU) | 1.9 |  8.3 |   8.0 | 1.5    | 0.8 | 448 x 448 | 24 |
| [InternVL3.5-2B](https://github.com/Qengineering/InternVL3.5-2B-NPU) | 3.0 |  22 |   8.0 | 2.7    | 0.8 | 448 x 448 | 11.2 |
| [InternVL3.5-4B](https://github.com/Qengineering/InternVL3.5-4B-NPU) | 5.4 |  50 |   8.0 | 5.9    | 0.8 | 448 x 448 | 5 |
| [InternVL3.5-8B](https://github.com/Qengineering/InternVL3.5-8B-NPU) | 8.8 |  92 |   8.0 | 50.5    | 5.8 | 448 x 448 | 3.5 |
| [Qwen2.5-3B](https://github.com/Qengineering/Qwen2.5-VL-3B-NPU) | 4.8 | 48.3 |  4.0 | 17.9  | 1.8 | 392 x 392 | 7.0 |
| [Qwen2-7B](https://github.com/Qengineering/Qwen2-VL-7B-NPU) | 8.7 | 86.6 |   34.5 | 37.1  | 20.7 | 392 x 392 | 3.7 |
| [Qwen2-2.2B](https://github.com/Qengineering/Qwen2-VL-2B-NPU) | 3.3 | 29.1 |   2.5 | 17.1  | 1.7 | 392 x 392 | 12.5 |
| [InternVL3-1B](https://github.com/Qengineering/InternVL3-NPU) | 1.3 |  6.8 |   1.1 | 7.8    | 0.75 | 448 x 448 | 30 |
| [SmolVLM2-2.2B](https://github.com/Qengineering/SmolVLM2-2B-NPU) | 3.4 | 21.2 |   2.6 | 10.5   | 0.9  | 384 x 384 | 11 |
| [SmolVLM2-500M](https://github.com/Qengineering/SmolVLM2-500M-NPU) | 0.8 |  4.8 |   0.7 | 2.5    | 0.25 | 384 x 384 | 31 |
| [SmolVLM2-256M](https://github.com/Qengineering/SmolVLM2-256M-NPU) | 0.5 |  1.1 |   0.4 | 2.5    | 0.25 | 384 x 384 | 54 |

<sup>1</sup> The total used memory; LLM plus the VLM. <br>
<sup>2</sup> When an llm/vlm model is loaded for the first time from your disk to RAM or NPU, it is called a cold start.<br>
The duration depends on your OS, I/O transfer rate, and memory mapping.<br> 
<sup>3</sup> Subsequent loading (warm start) takes advantage of the already mapped data in RAM. Mostly, only a few pointers need to be restored.<br><br>
<img width="1000" height="700" alt="Plot_Tokens" src="https://github.com/user-attachments/assets/7342debe-769c-46c9-8a83-755caf7d67dc" /><br>
<img width="1000" height="700" alt="PlotMemory" src="https://github.com/user-attachments/assets/cf4362e6-f644-46d3-9b74-d129b23d3c44" />

------------

## Dependencies.
To run the application, you have to:
- OpenCV 64-bit installed.
- rkllm library.
- rknn library.
- Optional: Code::Blocks. (```$ sudo apt-get install codeblocks```)

### Installing the dependencies.
Start with the usual 
```
$ sudo apt-get update 
$ sudo apt-get upgrade
$ sudo apt-get install cmake wget curl
```
#### OpenCV
To install OpenCV on your SBC, follow the Raspberry Pi 4 [guide](https://qengineering.eu/install-opencv-on-raspberry-64-os.html).<br><br>
Or, when you have no intentions to program code:
```
$ sudo apt-get install libopencv-dev 
```
------------

## Installing the app.
```
$ git clone https://github.com/Qengineering/Qwen3-VL-4B-NPU
```

#### RKLLM, RKNN
To run InternVL3, you need to have the **rkllm-runtime** library version **1.3.0** installed, as well as the **rknpu driver** version **0.9.8**.<br>
If you don't have these on your machine, or if you have a lower version, you need to install them.<br>
We have provided the correct versions in the repo.<br>
```bash
$ cd ./Qwen3-VL-4B-NPU/aarch64/library
$ sudo cp ./*.so /usr/local/lib
$ cd ../include
$ sudo cp ./*.h /usr/local/include
```

Your rkllm model must match the library.<br><br>
<img width="818" height="219" alt="RK_OK2" src="https://github.com/user-attachments/assets/cabb346b-a9fa-4c4f-9b3e-1ff785ce45fd" /><br><br>
If you use a model synthesized with the previous 1.2.3 rkllm library and run it with the latest 1.3.0, you will get a malfunction. The internal Byte-Pair Encoding (BPE) dictionary parsing gets misaligned.<br><br>
<img width="817" height="219" alt="RK_ERROR2" src="https://github.com/user-attachments/assets/bc9fad2a-8a1f-44f9-ab04-f834bb243f4c" />
<br>


## Download the LLM and VLM models.
The next step is downloading the models.<br>
Both can be downloaded from our [Hugging Face page](https://huggingface.co/Qengineering/Qwen3.5-4B-rk3588).<br>
- qwen3.5-4b_w8a8_rk3588.rkllm
- qwen3.5-4b-vision_rk3588.rknn
  
Copy both into this folder.


## Building the app.
Once you have the two models, it is time to build your application.<br>
You can use **Code::Blocks**.
- Load the project file *.cbp in Code::Blocks.
- Select _Release_, not Debug.
- Compile and run with F9.
- You can alter command line arguments with _Project -> Set programs arguments..._ 

Or use **Cmake**.
```
$ mkdir build
$ cd build
$ cmake ..
$ make -j4
```

## Running the app

The application switches dynamically between Single Image Mode and Video Sequence Mode based on how many image files you pass into the arguments.

```bash
./VLM_NPU RKNN_model RKLLM_model file1.jpg [file2.jpg file3.jpg ...]
```


| Argument | Comment |
| --- | --- |
| RKNN_model | The visual encoder model (VLM) compiled for the NPU. |
| RKLLM_model | The large language model (LLM) compiled for the NPU. |
| file1.jpg ... | The images you want to process.<br>Passing 1 file triggers **Image Mode**.<br>Passing multiple files triggers **Video Sequence Mode**. |

In the context of the Rockchip RK3588 LLM (Large Language Model) library, `NewTokens` and `ContextLength` control the boundaries for text generation and memory allocation.<br><br>
In `main.cpp` you will find the line:<br>  
```cpp
RKLLM.LoadModel(vlm_model, llm_model, NewTokens, ContextLength);
```
Here you set your context based on available memory.<br><br>
**NewTokens**
This sets the maximum number of tokens (pieces of text, typically sub-word units) that the model is allowed to generate in response to a prompt during a single inference round. For example, if set to 300, the model will not return more than 300 tokens as output, regardless of the prompt length. It is important for controlling generation length to avoid run-on responses and manage resource use.<br><br>
**ContextLength (Dynamic KV Cache)**
This specifies the maximum total number of tokens the model can hold in its memory at once, which includes the system prompt, the massive image/video embeddings, your text questions, and all previous generated answers.<br>
We have synthesized the models with a larger KV Cache than normal. Ours can hold up to **16384** tokens!
* **For 32GB Boards (e.g., Rock 5C 32GB):** You can safely push the KV Cache to `8192` or `16384` to support processing long video sequences and maintaining deep, multi-turn conversations without the model forgetting the image.
`RKLLM.LoadModel(vlm_model, llm_model, 2048, 16384);`

* **For 8GB/16GB Boards:** The KV cache is highly memory-intensive. You should keep this at `2048` or `4096`. If you set this higher than your physical RAM can handle, the Linux Out-Of-Memory (OOM) killer will crash the application.
`RKLLM.LoadModel(vlm_model, llm_model, 2048, 4096);`


**Typical Command Line Examples:**

Single Image Mode:

```bash
./VLM_NPU ./models/qwen3.5-4b-vision_rk3588.rknn ./models/qwen3.5-4b_w8a8_rk3588.rkllm ./frame1.jpg 

```

Video Sequence Mode (Passing multiple frames):

```bash
./VLM_NPU ./models/qwen3.5-4b-vision_rk3588.rknn ./models/qwen3.5-4b_w8a8_rk3588.rkllm ./frame1.jpg ./frame2.jpg ./frame3.jpg

```
##### ❗Showstopper❗
To process video input, individual frames are first extracted. The VLM converts each frame into embeddings, which are then transformed into vision tokens.<br>
Even on a desktop PC, this process places a heavy load on memory and CUDA resources. It’s therefore no surprise that the Rock 5C, with its more limited hardware, struggles even more.<br>
Each vision token corresponds to about 200 tokens, strongly limiting the number of frames processed per video. Therefore, the video is subsampled, and evenly spaced frames are extracted for processing by Qwen3.5.<br>
For reference, each vision token occupies around 20 MB of RAM — a detail worth keeping in mind when working on systems with limited memory.<br>
Keep also in mind that after loading the models, each frame has to be tokenised, which takes about 0.9 seconds per frame.

## Using the app

Using the application is simple. Once you provide the model and the media files, you can ask anything you want.<br>
Remember, we are on a bare Rock 5C, so don't expect the same speed or quality as massive server-grade models like ChatGPT. On the other hand, as you will see in the examples below, the app performs amazingly well on the edge!

**Interacting with Media:**

* If you passed a **single image** and want to talk about it, you must include the `<image>` tag in your prompt. (e.g., `"Describe this <image> in detail."`)
* If you passed **multiple images (video sequence)**, you must use the `<video>` tag instead. (e.g., `"What action is happening in this <video>?"`)

**Chat Controls:**

* The app remembers the dialogue context continuously. To wipe the model's memory and start a fresh conversation about the loaded media, type `clear`.
* To leave the application, type `exit`.

## C++ code.  
Below, you find the surprisingly little code of main.cpp. 
```cpp
#include "RK35llm.h"
#include <vector>

int main(int argc, char** argv)
{
    // Usage: ./VLM_VIDEO_NPU vlm_model llm_model frame1.jpg [frame2.jpg frame3.jpg ...]
    if (argc < 4) {
        std::cerr << "Usage: " << argv[0] << " vlm_model llm_model file1.jpg [file2.jpg file3.jpg ...]\n"; 
        return -1;
    }

    std::string vlm_model = argv[1];
    std::string llm_model = argv[2];

    RK35llm RKLLM;
    RKLLM.SetInfo(true);
    RKLLM.SetSilence(false);

    RKLLM.LoadModel(vlm_model, llm_model, 2048, 16384);

    // Collect all image frames from arguments
    std::vector<cv::Mat> frames;
    for (int i = 3; i < argc; ++i) {
        cv::Mat frame = cv::imread(argv[i]);
        if (!frame.empty()) {
            frames.push_back(frame);
        } else {
            std::cerr << "Warning: Could not load image file: " << argv[i] << "\n";
        }
    }

    if (frames.empty()) {
        std::cerr << "Error: No valid images loaded. Exiting.\n";
        return -1;
    }

    // Dynamic routing: single image vs. video sequence
    if (frames.size() == 1) {
        std::cout << "\n[Info] Loading single image mode...\n";
        RKLLM.LoadImage(frames[0]);
    } else {
        std::cout << "\n[Info] Loading video sequence mode (" << frames.size() << " frames)...\n";
        RKLLM.LoadVideoFrames(frames);
    }

    std::string input_str;
    std::string output_str;

    while (true) {
        printf("\nUser: ");
        std::getline(std::cin, input_str);
        if (input_str == "exit") break;

        // Reminder: the user must input the correct tag (<image> or <video>) based on the mode!
        output_str = RKLLM.Ask(input_str);
//        std::cout << "\nLLM Reply: " << output_str << std::endl;    }

    return 0;
}
```
Most code speaks for itself. One remark.<br>
The LLM generates the answer to your request in little pieces of text. You see them as if the LLM is typing on your terminal.<br>
RKLLM.SetSilence controls this behaviour. When set to `true`, it will suppress this output. RKLLM.Ask() also returns the complete answer.<br>
In main.cpp uncomment this line:
```cpp
std::cout << "\nLLM Answer: " << output_str << std::endl;
```

------------

## VLM examples.
| Image         | Dialog |
| --------------| --  |
| ![Singapore_S](https://github.com/user-attachments/assets/e742059a-3bdb-41be-9647-e7767da12ce6) |**User**: \<image\>Which city is this?<br>**Answer**: This is **Singapore**.<br>The image shows the iconic skyline of Singapore at dusk or twilight, featuring:<br>- The **Marina Bay Sands** hotel on the left — recognizable by its three towers connected by a skybridge and distinctive roof structure.<br>- The **Singapore Flyer**, one of the world’s largest observation wheels, located in Marina Bay.<br>- Other modern skyscrapers along the waterfront, including the **Esplanade – Theatres on the Bay** (the two white shell-shaped buildings) near the center.The calm water in the foreground reflects the city lights and sky, capturing the serene yet vibrant atmosphere of this global hub.<br>✅ So, the answer is: **Singapore**. | 
| ![ChineseWall_S](https://github.com/user-attachments/assets/3ba4b57a-4b22-4050-b995-9599c6d239de) |**User**: \<image\>Tell me something about the history of this place.<br>**Answer**: This image shows a section of the **Great Wall of China**, one of the most iconic and historically significant structures in human history — stretching over 21,000 kilometers (13,000 miles) across northern China’s rugged terrain.<br><br>**Historical Background:**<br>The Great Wall was not built all at once but evolved over centuries under different dynasties. Its construction began as early as the **Warring States Period (475–221 BCE)**, when individual states like Qin, Yan, and Zhao built defensive walls to protect against nomadic invasions from the north — particularly the Xiongnu confederation.<br>The most famous phase of its construction occurred under the **Qin Dynasty (221–206 BCE)**. After unifying China, Emperor Qin Shi Huang ordered the connection and expansion of existing state walls into a continuous defensive system. He also added watchtowers, barracks, and fortified passes — laying the foundation for what we now recognize as the Great Wall.<br>Later dynasties — especially the **Ming Dynasty (1368–1644)** — significantly expanded and reinforced the wall with brick-and-stone construction, adding more towers, battlements, and strategic fortifications. The Ming-era sections are often the ones tourists see today because they’re better preserved and more visually dramatic.<br><br>**Purpose:**<br>- **Defense**: To repel invasions by nomadic tribes from the steppes.<br>- **Control**: To regulate trade and movement along the northern frontier.<br>- **Symbolism**: It represented imperial power, unity, and resilience.<br><br>**Legacy:**<br>Today, parts of the Great Wall are UNESCO World Heritage Sites (e.g., Badaling, Mutianyu, Jinshanling). They stand as monumental testaments to ancient engineering prowess and enduring cultural identity. Despite centuries of war, natural erosion, and neglect, many sections remain intact — some even accessible for hiking or photography like in your image.<br><br>In short: This wall isn’t just a barrier — it’s a story of survival, strategy, and human perseverance carved into the landscape over two millennia. 🏯🧱⛰️|
| ![Pizza_S](https://github.com/user-attachments/assets/26fd5da3-f491-4b48-978a-14eae0819247) |**User**: \<image\>What are the ingredients I need to make this?<br>**Answer**:To recreate this pizza — which appears to be a classic **Neapolitan-style Margherita** with fresh basil and charred crust — you’ll need:<br><br>🍕 **Ingredients:**<br>**Dough (for 1 small Neapolitan pizza):**<br>- 250g (about 9 oz) “00” flour (Italian bread flour or high-protein all-purpose works too)<br>- 375ml (1¼ cups) warm water (adjust slightly based on hydration — aim for ~68% hydration)<br>- 7–8g active dry yeast (or instant yeast)<br>- 2 tsp sea salt<br> *Optional:* A pinch of sugar or honey to help yeast activate.<br><br>**Sauce:**<br>- 1 cup San Marzano tomato sauce (canned whole peeled tomatoes crushed by hand, strained if needed)<br>- Optional: 1 clove garlic, minced (optional — traditional Margherita often omits it)<br>- Freshly cracked black pepper or red pepper flakes (optional)<br><br>**Cheese:**<br>- 200g fresh mozzarella di bufala (buffalo mozzarella), sliced thin OR low-moisture whole milk mozzarella balls (bocconcini), torn into pieces <br>*Tip:* Use low-moisture for easier handling; buffalo gives richer flavor.<br><br>**Toppings:**<br>- Fresh basil leaves, torn by hand (not pre-chopped — you want big, vibrant leaves)<br>- Optional: A drizzle of extra virgin olive oil before baking<br><br>🔥 **Equipment Needed:**<br>- Pizza stone or steel (preheat in oven to highest setting + broil on high for last 5–10 mins)<br>- Baking sheet lined with parchment paper (if no stone/steel)<br>- Peeler or knife to score dough before baking<br>- Tongs or peel to transfer pizza<br><br>🧑‍🍳 **Quick Instructions:**<br>1. **Make Dough:** Mix flour, yeast, salt, and water until shaggy. Let rise 2–4 hours (or overnight in fridge).<br>2. **Preheat Oven + Stone/Steel:** Set oven to max heat (~500°F / 260°C or higher if possible), broil on high for last 10 mins.<br>3. **Prepare Sauce & Cheese:** Mix sauce; set aside cheese and basil.<br>4. **Shape Dough:** Punch down dough, stretch gently into round (don’t overwork!). Transfer to parchment-lined sheet.<br>5. **Add Toppings:** Spread sauce lightly, add mozzarella, top with fresh basil leaves.<br>6. **Bake:** Slide onto hot stone/steel or baking sheet. Bake 8–12 minutes until crust is puffed and charred in spots, cheese bubbly.<br>7. **Finish:** Drizzle with EVOO if desired. Serve immediately!<br><br>💡 Pro Tips:<br>- Let dough rest after shaping to relax gluten before baking.<br>- Don’t overcrowd toppings — let them breathe for even cooking.<br>- For authentic char, use a very hot oven and broil at the end.<br><br>Enjoy your homemade Neapolitan Margherita! 🍕✨<br><br>**User**:What is the first step?<br>**Answer**:The **first step** to making this pizza is:<br>**Prepare the dough.**<br>This means mixing together:<br>- 250g “00” flour (or high-protein all-purpose)<br>- 375ml warm water<br>- 7–8g active dry yeast<br>- 2 tsp sea salt<br><br>Mix until a shaggy dough forms, then let it rise for at least 2 hours (or overnight in the fridge). This gives you the foundation for that charred, airy Neapolitan crust.<br><br>Once the dough is ready and risen, you can move on to making the sauce, cheese, and assembling the pizza.<br><br>✅ So — **Step 1: Make and let rise your pizza dough.**|
| ![Titanic_S](https://github.com/user-attachments/assets/bf6da76c-c9a4-41c6-bea1-2b4411dd4013) |**User**: \<image\>Which movie is this?<br>**Answer**:This iconic scene is from the 1997 romantic drama film **Titanic**.<br>The image shows Leonardo DiCaprio (as Jack Dawson) and Kate Winslet (as Rose DeWitt Bukater) on the bow of the RMS Titanic, arms outstretched toward a sunset — one of the most famous and emotionally resonant moments in cinema history. It symbolizes their brief but transformative love story aboard the ill-fated ship.<br>The film was directed by James Cameron and became a global phenomenon, earning multiple Academy Awards including Best Picture.|

## Video example.
![Sequence](https://github.com/user-attachments/assets/1e6af4e2-cdc4-4e22-868a-82e3df34fbb7)<br>
**User**: \<video\> Describe the video.<br>
**Answer**: The video shows a man practicing martial arts in what appears to be a dojo or training hall with tatami mats on the floor and calligraphy scrolls hanging on light blue walls. The sequence captures him performing a dynamic move, possibly a kick or flip, which results in him falling onto his back as he completes the motion. His attire consists of dark clothing suitable for martial arts practice.  

## LLM example.
Notice the nice Markdown makeup of the answer!<br><br>
**User**: Can you make me a C++ call that embeds the Pythagorean theorem?<br><br>
**Answer**: Sure! Here's a simple and clear C++ program that demonstrates the **Pythagorean theorem**:  
> \( a^2 + b^2 = c^2 \)  
where `c` is the hypotenuse of a right triangle, and `a`, `b` are the other two sides.

```cpp
#include <iostream>
#include <cmath>   // for std::sqrt()
using namespace std;

int main() {
    double a, b, c;

    cout << "Enter side 'a': ";
    cin >> a;

    cout << "Enter side 'b': ";
    cin >> b;

    // Calculate hypotenuse using Pythagorean theorem: c = sqrt(a² + b²)
    c = sqrt(pow(a, 2) + pow(b, 2));

    cout << "\nHypotenuse (c) = " << c << endl;

    return 0;
}
```

### How it works:
- Uses `pow(base, exponent)` to square the sides.
- Uses `sqrt()` from `<cmath>` to compute the square root of the sum.
- Prompts user for two legs (`a` and `b`) and outputs the hypotenuse (`c`).

### Example Run:
```
Enter side 'a': 3
Enter side 'b': 4

Hypotenuse (c) = 5
```

Let me know if you’d like to add validation, handle non-right triangles, or make it a function-based design! 📐✨

------------

## **[Rock5GPT](https://rock5gpt.qengineering.eu)**
To get a taste, try our professional Qwen3 AI-chatbot running on a Rock 5C: https://rock5gpt.qengineering.eu
<img width="815" height="1151" alt="Rock5GPT" src="https://github.com/user-attachments/assets/3ce5ad31-bc2b-4513-8ac9-42be793a86db" /><br>

------------

[![paypal](https://qengineering.eu/images/TipJarSmall4.png)](https://www.paypal.com/cgi-bin/webscr?cmd=_s-xclick&hosted_button_id=CPZTM5BB3FCYL) 




