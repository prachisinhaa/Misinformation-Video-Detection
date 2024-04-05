# Misinformation-Video-Detection
Final project for the Computer Vision course 

Video-based misinformation brings new and unique challenges to automatic detection systems:
1) high information heterogeneity brought by various modalities, 
2) blurred distinction between misleading video manipulation and nonmalicious artistic video editing, and 
3) new patterns of misinformation propagation due to the dominant role of recommendation systems on online video platforms. 

We first analyze and characterize the misinformation video from three levels including signal, semantic, and intent. Based on the characterization, we systematically review existing works for detection from features of various modalities to techniques for clue integration.

For individuals, misinformation videos are more likely to mislead audiences to generate false memory and make misinformed decisions. For online platforms, the wide spread of misinformation videos may lead to reputation crises, users’ inactivity, and regulatory checks. For watchdog bodies, misinformation videos may be weaponized to foment unrest and even undermine democratic institutions.

Challenges: 
Despite many valuable surveys conducted on broad misinforma- tion detection, limited attention is given to video-based misinformation. Most of them regard the video as a kind of visual content as the image and discuss general multi-modal techniques for misin- formation detection









### Main contributions made by paper:

> Comprehensive characterization:
present a comprehensive analysis of characteristics of misinformation videos from three levels including signal, semantic, and intent;

> Systematic technical overview: 
provide a systematical overview of existing multimodal detection techniques and methods for misinformation in the video form with a principled way to group utilized clues and integration mechanisms;

> Concrete future directions: 
discuss several open issues in this area and provide concrete future directions for both research and real-world application scenarios.



## 2. MISINFORMATION VIDEO CHARACTERIZATION
Definition 2.1 (Misinformation Video). A video post that conveys false, inaccurate, or misleading information.
### 2.1 Signal Level
> Misinformation videos often contain manipulated or generated video and audio content in which the forgery procedure often leads to traces in underlying digital signals. Forgery methods that produce such traces can be classified into two groups: Editing and Generation.
### 2.2 Semantic Level
> The falsehood is conveyed through incorrect semantic changes against the truth. For a misinformation video, such changes may occur in one specific modality or across multiple ones. For instance, a creator may upload a real video of an event that happened before but add a real text description of a newly emerging event.
### 2.3 Intent Level
> The creation of misinformation is often motivated by underlying intents, such as political influence, financial gain, and propaganda effects



## 3. MISINFORMATION VIDEO DETECTION
The misinformation video detection problem is formulated as a binary classification task: Let V and S denote a Video and attached Social Context, respectively. 
V = attributes such as title/description 𝑡, video 𝑣, and audio 𝑎.
𝑆 = two major components: User Profile 𝑝 and User Engagement 𝑒. 
User Profile 𝑝 includes a set of features to describe the uploader account, such as the location indicated by IP address, self-written and verified introduction, and follower count. 
User Engagement 𝑒 includes comments as well as statistics such as the number of views, likes, and stars. Fig. 1 illustrates an example of V from TikTok. The task of misinformation video detection is to predict whether the video post V contains misinformation given all the accessible features E = {V, S}, i.e., F : E ↦→ {0, 1}.

### 3.1 Signal Level
The detection of video forgery traces would provide a significant clue for detecting a misinformation video.
#### 3.1.1 Editing Traces. 
> Existing detection methods for editing traces can be mainly categorized into two groups: active detection and passive detection.
In active detection methods, digital watermarks or digital signatures are pre-embedded and extracted to detect the trace of secondary editing. They provide quicker responses and more accurate judgments than passive detection.
The passive detection methods use the characteristics of the digital video itself to detect tampering traces. For video frames, tampering detection methods leverage inter-frame and intra-frame information. 
 inter-frame: detects the abnormal change in frame sequences, such as insertion, deletion, duplication, and shuffling of frames.
intra-frame : detects the alteration of objects that could be reflected in a single frame, such as region duplication and splicing. 
#### 3.1.2 Generation Traces. 
> Most existing works for fake audio detection adopt hand-crafted acoustic features like Mel-frequency cepstral coeffi- cients (MFCC), linear frequency cepstral coefficient (LFCC), and constant-Q cepstral coefficients (CQCC) and apply classifiers such as Gaussian mixture model and light convolutional neural network to make predictions. Recent work also attempts to leverage pre- trained wav2vec-style models for speech representation extraction and build an end-to-end framework

### 3.2 Semantic Level
Though signal-level clues could provide strong evidence, they are not decisive because of the wide use of portable editing tools.
 The existence of semantically unchanged edited videos has blurred the boundary between fake and real videos. For instance, a video edited for the sake of brevity/clarity may still be truthful. Conversely, an untampered video can be employed in a deceptive manner. 
Semantic-level clues offer a new perspective for identifying misinformative content. Thus, many recent works focus on leveraging multi-modal semantic clues from not only the video content but also descriptive textual information.
#### 3.2.1 Textual Feature. 
> The video content is always served with descriptive textual information such as video description, and title. Apart from these directly accessible texts, subtitles and transcriptions extracted from the video also present useful information.
#### 3.2.2 Visual Feature. 
> The visual content is usually represented at the frame level or clip level. The former presents static visual features while the latter presents additional temporal features. 
#### 3.2.3 Acoustic Feature. 
> As a unique modality compared to text-image misinformation, the audio modality including speech, environment sound, and background music, plays an essential role in expressing information in videos. 
#### 3.2.4 Cross-modal Correlation. 
> Mismatches between modalities, such as video-text and video-audio, are often caused by video repurposing for the misleading aim, which would lead to important changes in cross-modal correlation


### 3.3 Intent Level
Starting from the motivations of those who create and spread misinformation, some effective features for detecting misinformation videos are leveraged by researchers.
User engagement statistics such as the number of likes, comments, and views are generally directly concatenated with other features before being put into the classifier
The publisher profile provides auxiliary information about source credibility in post-level detection.
leverage a series of features, such as the number of views of the publisher channel, number of published videos, and follower-following ratio
user profiling features like geolocation information and whether the account is verified or not can be useful to the detection, and exploit the textual publisher description in their model.

### 3.4 Clue Integration
#### 3.4.1 Parallel Integration.
> In parallel integration, all clues from different modalities contribute to the final decision-making process, although their participation may not be equal. The integration process can be performed at both the feature level (where features from different modalities are fused before being input into the classifier) and the decision level (where predictions are produced independently by different branches and combined using strategies like voting for final decisions).
Concatenation-Based: The majority of the existing works on multi-modal misinformation detection embed each modality into a representation vector and then concatenate them as a multi-modal representation. 
Attention-Based: The attention mechanism is a more effective approach for utilizing embeddings of different modalities, as it jointly exploits the multi-modal feature by focusing on specific parts and allows dynamic fusion for sequential data.
Multitask-Based: Under this architecture, auxiliary networks are applied to learn individual or multi-modal representations, spaces, or parameters better and improve the classification per- formance [2]. For example, Choi and Ko [13] use a topic-adversarial classification to guide the model to learn topic-agnostic features for good generalization. Wang et al. [73] use contrastive learning to build the joint representation space of video and text.
#### 3.4.2 Sequential Integration. 
> In sequential integration, clues from different modalities are combined in a stepwise manner with each modality contributing incrementally to the final decision. This way of integration can promote overall efficiency and effectiveness, especially when some modalities provide redundant or overlapping information.





## 4. Resources
### 4.1 Datasets

YouTubeAudit3. This dataset contains 2,943 videos that were published in 2020 on YouTube and cover five popular misinformative topics. Each sample is labeled as promoting, debunking, and neutral to misinformation. It also provides social contexts like metadata (e.g., video URL, title, duration), statistics of user engagements, and user profiles (e.g., gender and age).

### 4.2 Tools
Tools for specific utilities are valuable for verifying suspicious videos because they provide important auxiliary information that could be hardly learned by a data-driven model. Three representative publicly available tools for different application contexts:

1. DeepFake Detector: An AI service to judge whether a given video contains deepfake manipulated faces, developed within WeVerify Project6. It uses the URL of a suspicious image or video as the input and returns the deepfake probability score. It could help detect generation traces discussed in Sec. 3.1.2.

2.  Reverse Image Search: Web search services with an image as a query. By submitting extracted keyframes, we could check if similar videos exist elsewhere before. This could help detect the manipulation by comparison and identify the original source, as discussed in Secs. 3.1 and 3.2. Many general search engines (e.g., Google and Baidu) provide such services. Task- specific tools include TinEye, ImageRaider, and Duplichecker7.

3. Video Verification Plugin: A Google Chrome extension to verify videos provided by the InVID European Project8. It provides a toolbox to obtain contextual information from YouTube or Facebook, extract keyframes for reverse search, show metadata



## References
> Paper: https://dl.acm.org/doi/pdf/10.1145/3581783.3612426

> Dataset: https://github.com/ICTMCG/Awesome-Misinfo-Video-Detection?tab=readme-ov-file#datasets
