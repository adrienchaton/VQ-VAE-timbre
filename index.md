<link href="style.css" rel="stylesheet">

<script type="text/javascript"> 
      // Show button
      function look(type){ 
      param=document.getElementById(type); 
      if(param.style.display == "none") param.style.display = "block"; 
      else param.style.display = "none" 
      } 
</script>


This webpage and repository host additional materials for the submission to ISMIR 2020 entitled "Vector-Quantized Timbre Representation". After the anonymized reviewing period, codes for our re-implementation of the perceptual audio loss will be merged into the final repository. Thank you for reading.


## Details of the mapping method for descriptor-based synthesis

Following the notations from the paper, we detail the procedure for mapping the discrete latent space with a signal descriptor. For instance acoustic properties such as centroid, bandwidth or fundamental frequency. And then using this mapping to control synthesis with a descriptor target. We call this descriptor-based synthesis, which is done without iterative search but with direct selection of the best matching latent features.

<p align="center"> <img src="figures/ISMIR_supplem.png"> </p>
