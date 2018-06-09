# OZIP
**Ozip** is a simple compression utility utilizing the Oodle high performance compression library.  Ozip's functionality mimics gzip; most invocations function identically. Like gzip, Ozip supports streaming compression/decompression from stdin to stdout. Builds on Windows, Linux and Mac.  
Ozip requires the Oodle SDK.  
# Usage    

ozip [file] [opts]             (compresses)  
ozip [file] [-d opts]          (decompress)  

* without file args ozip defaults to stdin/stdout compression.  
* uses .ooz extension for compressed files.  
* (!)Deletes input files unless -k --keep opt is used (as does gzip).  
* Ozip iterates on multiple file targets. To combine files, compose with tar (e.g. tar <files> | ozip > "archivedfiles.tar.ooz")

Default compression settings are Oodle Kraken at Compression Level Normal (4).  

# Settings  
Compressor selection:  
                      --kraken -mk  
                      --leviathan -ml  
                      --selkie -ms  
                       --mermaid -mm  
               	       --hydra -mh  
*Kraken provides a balance of ratio and speed.   
Leviathan provides maximum compression.    
Selkie and Mermaid are even faster.                    
Hydra can hit performance targets between those choices.  
For more info see http://www.radgametools.com/oodlecompressors.htm*  

		       
compression effort level:     
          -1 -2  ...  -8  
*Higher effort levels get a better compression ratio at the expense of encode time*

More Options:  

     		-H                     
		*prints Oodle compressor options help*  
 		-c --stdout	        
		*outputs to stdout (decompress only).*    
 		-d --decompress         
		*decompress*   
 		-z --compress           
		*compress*  
 		-k --keep               
		*keep original file (otherwise deleted)*      
  		-f --force              
		*overwrite output file if exists *  
 		-F --fast              
		*low latency streaming compression*  
 		-b --best              
		*best compression. Long compress times.*  
 		-t --test              
		*tests existing compressed file validity*    
 		-K --verify           
		*verify file during compression*     
 		-q --quiet           
		*no prints*  
 		-v --verbose         
		*prints lots*  
 		-s --small          
		*low memory use ~2.5MB  (compression only)*   
 		-(1-9)	                
		*compression level 1-9*  
 		-m[k] --compressor=[k] 
		*[k/l/m/s] Oodle compressor selection*  
 		--kraken --mermaid --selkie --leviathan     *Oodle compressor choice*    
 		--bufferlimit=[1-256]  
		*(MB) max buffer size for compression.*  
 		--blocklimit=[8+]      
		*(KB) minimum block size in KB for streaming*  
  		--contextlimit=[8+]     
		*(KB) context limit KB. trades memory use for ratio*   
Unix only:   
 		--timeout=[1000]        
		*time in ms to wait on inactve stdin during compression*  
		

Additional Oodle Compression options displayed with -H. See the Oodle Data Documentation for details.   

# Headers 

Ozip adds a file header and block header to compressed data stream. Values are little endian.
File Header Version 1:   16 bytes.    4 byte "OZIP" magic word. 4 byte Header Version. 8 byte filesize (if known.)
Block Header Version 1:  16 bytes.    4 byte "OZIP" magic word. 4 bytes raw block size. 4 bytes context size. 4 bytes compressed size.

# About   
OZIP ver. 0.0.7   

Ozip developed by:   
https://github.com/jamesbloom/ozip   
jamesbloom@gmail.com    
    
About the Oodle SDK:    
http://www.radgametools.com/oodle.htm   
    
