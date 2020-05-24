<!--
<audio controls><source src="audio/rec_drum.wav"></audio>
-->

<!--
<link href="style.css" rel="stylesheet">
-->

<script type="text/javascript"> 
      // Show button
      function look(type){ 
      param=document.getElementById(type); 
      if(param.style.display == "none") param.style.display = "block"; 
      else param.style.display = "none" 
      } 
</script>

&nbsp;

**The page display depends on the browser used (e.g. audio players). All audio samples are located in https://github.com/anon-248/VQ-VAE-timbre/tree/master/audio ; please leave us an issue if the page is not showing properly.**

&nbsp;


## Details of the mapping method for descriptor-based synthesis

Following the notations from the paper, we detail the procedure for mapping the discrete latent space with a signal descriptor. For instance acoustic properties such as centroid, bandwidth or fundamental frequency. And then using this mapping to control synthesis with a descriptor target. We call this *descriptor-based synthesis*, which is done without iterative search but with direct selection of the best matching latent features. The operator that we call *descriptor* can be any signal descriptors, we use the spectral features implemented in [librosa](https://librosa.github.io/librosa/feature.html#spectral-features). Fundamental frequency estimate is computed with the [PyWorldVocoder](https://github.com/JeremyCCHsu/Python-Wrapper-for-World-Vocoder).

&nbsp;

<p align="center"> <img src="figures/ISMIR_supplem.png"> </p>

&nbsp;

The mapping is performed with the following analysis.

&nbsp;

<p align="center"> <img src="figures/descriptor_ana.png"> </p>

&nbsp;

Descriptor-based synthesis can be done using the mapping to a given acoustic descriptor target. Red denotes the controllable synthesis parameters.

&nbsp;

<p align="center"> <img src="figures/descriptor_map.png"> </p>

&nbsp;

## Timbre transfer

The model can be used for timbre transfer from diverse sources, including non-musical sounds such as vocal imitations, to an invidual timbre. It learns a discrete representation of the trained timbre, a latent codebook into which any encoder outputs is matched. For instance, an input audio of a clarinet performance can be quantized into latent features learned from a violin dataset. Subsequently, the decoder synthesizes an audio that is the closest match to the input given the target timbre features.

&nbsp;

<p align="center"> <img src="figures/transfer.png"> </p>

&nbsp;



## Audio samples from the models

*Page and repository in progress. Demonstration materials are uploaded within the next days.*

One VQ-VAE model has been trained per individual timbre domain. The corresponding datasets are either isolated instrument performances from multitrack recordings (URMP, Phenicx) or singing voice (subset of VocalSet). The instruments of the orchestra are: basson, cello, clarinet, double-bass, flute, horn, oboe, trumpet, viola and violin.

&nbsp;

### Descriptor-based synthesis

To demonstrate to possiblity to control synthesis from some acoustic descriptor targets, we analyze the VQ-VAE discrete latent space and traverse the latent codes in an increasing order with respect to different descriptors. As explained in the upper details, we can use the sorted codebook to map with some user-defined descriptor targets. We provide the sound output as well as the spectrogam and descriptor curve that have been synthesized.

| **bandwidth in cello** | <audio controls><source src="audio/desc_based/cello_bandwidth.wav"></audio> |
|  :---:  | :---:  |
|  <p align="center"> <img src="audio/desc_based/cello_bandwidth_desc.png"> </p>  |  <p align="center"> <img src="audio/desc_based/cello_bandwidth_spec.png"> </p> |

&nbsp;

### Timbre transfer

A model is trained on a target timbre, we input performance excerpts from other sources (unseen during training) and transfer them to the learned target timbre.

| instruments | source | target |
|  :---:  | :---:  | :---:  |
|**clarinet → trumpet**|  <audio controls><source src="audio/timbre_transfer/clarinet_to_trumpet_src.wav"></audio> | <audio controls><source src="audio/timbre_transfer/clarinet_to_trumpet_out.wav"></audio>|
|**clarinet → violin**|  <audio controls><source src="audio/timbre_transfer/clarinet_to_violin_src.wav"></audio> | <audio controls><source src="audio/timbre_transfer/clarinet_to_violin_out.wav"></audio>|
|**horn → cello**|  <audio controls><source src="audio/timbre_transfer/horn_to_cello_src.wav"></audio> | <audio controls><source src="audio/timbre_transfer/horn_to_cello_out.wav"></audio>|
|**horn → singing**|  <audio controls><source src="audio/timbre_transfer/horn_to_singing_src.wav"></audio> | <audio controls><source src="audio/timbre_transfer/horn_to_singing_out.wav"></audio>|
|**oboe → viola**|  <audio controls><source src="audio/timbre_transfer/oboe_to_viola_src.wav"></audio> | <audio controls><source src="audio/timbre_transfer/oboe_to_viola_out.wav"></audio>|
|**saxophone → cello**|  <audio controls><source src="audio/timbre_transfer/saxophone_to_cello_src.wav"></audio> | <audio controls><source src="audio/timbre_transfer/saxophone_to_cello_out.wav"></audio>|
|**saxophone → horn**|  <audio controls><source src="audio/timbre_transfer/saxophone_to_horn_src.wav"></audio> | <audio controls><source src="audio/timbre_transfer/saxophone_to_horn_out.wav"></audio>|
|**singing → violin**|  <audio controls><source src="audio/timbre_transfer/singing_to_violin_src.wav"></audio> | <audio controls><source src="audio/timbre_transfer/singing_to_violin_out.wav"></audio>|
|**trumpet → clarinet**|  <audio controls><source src="audio/timbre_transfer/trumpet_to_clarinet_src.wav"></audio> | <audio controls><source src="audio/timbre_transfer/trumpet_to_clarinet_out.wav"></audio>|
|**trumpet → singing**|  <audio controls><source src="audio/timbre_transfer/trumpet_to_singing_src.wav"></audio> | <audio controls><source src="audio/timbre_transfer/trumpet_to_singing_out.wav"></audio>|

&nbsp;

### Voice-driven sound synthesis

Besides converting singing voice into an instrument sound, we also consider inputting non-singing human voice. We take some samples from the VocalSketch database, these were crowd-sourced in uncontrolled recording conditions by asking participants to immitate some diverse targets with their voice. Such concepts would be hardly described into musical terms, however they are rather intuitively expressed by vocal imitation. This can be a new mean to drive a sound synthesis model, which do not require any particular knowledge for interaction. The first sample is a raw vocal imitation and the second a transfer to an instrument timbre. *Concept* refers to the text descriptions in VocalSketch that were given to imitate.

| concept → instrument | input | transfer |
|  :---:  | :---:  | :---:  |
| **aliendiscovery → viola** | <audio controls><source src="audio/voice_driven/aliendiscovery_to_viola_src.wav"></audio> | <audio controls><source src="audio/voice_driven/aliendiscovery_to_viola_out.wav"></audio> |
| **banjo → cello** | <audio controls><source src="audio/voice_driven/banjo_to_cello_src.wav"></audio> | <audio controls><source src="audio/voice_driven/banjo_to_cello_out.wav"></audio> |
| **bongos → horn** | <audio controls><source src="audio/voice_driven/bongos_to_horn_src.wav"></audio> | <audio controls><source src="audio/voice_driven/bongos_to_horn_out.wav"></audio> |
| **cashregister → clarinet** | <audio controls><source src="audio/voice_driven/cashregister_to_clarinet_src.wav"></audio> | <audio controls><source src="audio/voice_driven/cashregister_to_clarinet_out.wav"></audio> |
| **cat → clarinet** | <audio controls><source src="audio/voice_driven/cat_to_clarinet_src.wav"></audio> | <audio controls><source src="audio/voice_driven/cat_to_clarinet_out.wav"></audio> |
| **crow → viola** | <audio controls><source src="audio/voice_driven/crow_to_viola_src.wav"></audio> | <audio controls><source src="audio/voice_driven/crow_to_viola_out.wav"></audio> |
| **darkattackbass → horn** | <audio controls><source src="audio/voice_driven/darkattackbass_to_horn_src.wav"></audio> | <audio controls><source src="audio/voice_driven/darkattackbass_to_horn_out.wav"></audio> |
| **feedback → violin** | <audio controls><source src="audio/voice_driven/feedback_to_violin_src.wav"></audio> | <audio controls><source src="audio/voice_driven/feedback_to_violin_out.wav"></audio> |

&nbsp;

### Test set reconstructions

The models are trained on recording segments of about 1.5 second, we show some examples from the test set of each timbre domain and the corresponding VQ-VAE reconstruction. The first sample for each is an input and the second is the model reconstruction.

| instrument | input | reconstruction |
|  :---:  | :---:  | :---:  |
|**basson**|  <audio controls><source src="audio/reconstructions/basson_in.wav"></audio> | <audio controls><source src="audio/reconstructions/basson_rec.wav"></audio>|
|**cello** | <audio controls><source src="audio/reconstructions/cello_in.wav"></audio> | <audio controls><source src="audio/reconstructions/cello_rec.wav"></audio>|
|**clarinet**|  <audio controls><source src="audio/reconstructions/clarinet_in.wav"></audio> | <audio controls><source src="audio/reconstructions/clarinet_rec.wav"></audio>|
|**double-bass**|  <audio controls><source src="audio/reconstructions/doublebass_in.wav"></audio> | <audio controls><source src="audio/reconstructions/doublebass_rec.wav"></audio>|
|**flute** | <audio controls><source src="audio/reconstructions/flute_in.wav"></audio> | <audio controls><source src="audio/reconstructions/flute_rec.wav"></audio>|
|**horn** | <audio controls><source src="audio/reconstructions/horn_in.wav"></audio> | <audio controls><source src="audio/reconstructions/horn_rec.wav"></audio>|
|**oboe**|  <audio controls><source src="audio/reconstructions/oboe_in.wav"></audio> | <audio controls><source src="audio/reconstructions/oboe_rec.wav"></audio>|
|**trumpet** | <audio controls><source src="audio/reconstructions/trumpet_in.wav"></audio> | <audio controls><source src="audio/reconstructions/trumpet_rec.wav"></audio>|
|**viola** | <audio controls><source src="audio/reconstructions/viola_in.wav"></audio> | <audio controls><source src="audio/reconstructions/viola_rec.wav"></audio>|
|**violin** | <audio controls><source src="audio/reconstructions/violin_in.wav"></audio> | <audio controls><source src="audio/reconstructions/violin_rec.wav"></audio>|
|**singing** | <audio controls><source src="audio/reconstructions/singing_in.wav"></audio> | <audio controls><source src="audio/reconstructions/singing_rec.wav"></audio>|
