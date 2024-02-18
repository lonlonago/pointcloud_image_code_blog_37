##  3D point cloud data annotation 

 There should be a lot of students who have just started to come into contact with 3D deep learning, have been arranged to label data work, find the right way to label is a very difficult thing, bloggers in the search for marking tools, almost tried all the current marking tools, such as the current more popular PCAT_Open_Source, Semantic-Segmentation-Editor, such software is excellent but there are some drawbacks, such as complex installation steps, the use of vague, for the new entry of scientific research Xiaobai is extremely unfriendly, Lidar360 contains a rich set of point cloud data processing tools, but can not be used for point cloud accurate labeling, there are some other not very mainstream labeling tools, but also almost all in the installation can not be used for labeling state. After comparison, CloudCompare was selected as the final labeling tool. The installation method is simple, the labeling process is clear, and the visual effect after labeling is intuitive. The following is a labeling tutorial written by the blogger, which has tried to prompt all the difficulties you may encounter. Please pay attention to the details and read the entire labeling tutorial before labeling to avoid mistakes. Scientific research is a delicate job, and so is labeling! 

##  Labeling tools 

 CloudCompare2.9.0 

 Download link: https://pan.baidu.com/s/1sjnu3pHXu-3vaRaK1LC8-g 

 Tutorial: https://blog.csdn.net/datase/article/details/79797795 

##  Labels 

##  III. Labeling steps 

 ![avatar]( 20200127090841292.png) 

 ![avatar]( 20200127091326778.png) 

 Check and click Data (in blue), if you don't click, you will not be able to box: Edit- > Segment Select the local area to be marked (green box): 

 ![avatar]( 20200127091342965.png) 

  Click the Segment in button at the top right to get the labeled area: 

 ![avatar]( 20200127091402841.png) 

 Click the Confirm Segmentation button to save: 

 ![avatar]( 2020012709141951.png) 

 The directory will have one more line of data for the part just cut: 

 ![avatar]( 20200127091423314.png) 

 Cancel the check of the original data, single-select the point cloud data of the cutting part, and the interface will only display the cutting part: 

 ![avatar]( 20200127091445633.png) 

 Toolbar operation: Edit - > Scalar fields - > Add constant SF input label: 

 ![avatar]( 20200127091613997.png) 

  If the labelid of the building is 4, fill in 4: 

 ![avatar]( 20200127091626636.png) 

  Click OK, and observe that the Count value under Scalar Fields becomes 7 (Count represents the number of scalars in the data, and the initial value of this data is 6. The following examples are based on 6. The actual situation refers to its own data set, and the initial value of each data is different.), and the marked buildings become blue: 

 ![avatar]( 20200127091642989.png) 

 ![avatar]( 20200127091658375.png) 

  Check All data to observe the display effect of the marked part in all data: this time the label is over. 

 To make a second annotation, just tick the unmarked data, not the already marked data, to prevent repeated annotations. It can be observed that the marked data is not displayed. 

 ![avatar]( 20200127091741540.png) 

 The Count value under the unlabeled data Scalar Fields must be 6 (the Count value of each data is different, here 6 is used as a benchmark for the initial Count), if not 6, consider whether in the process of annotation of the framed data, the unframed data part is also checked. Solution: Select the unlabeled data, Edit - > Scalar fields - > Delete, and the Count of Scalar fields will change from 7 to the initial 6. 

 ![avatar]( 20200127091824909.png) 

  Repeat the 3.2 operation, frame the road surface, and get the following figure: 

 ![avatar]( 20200127091837111.png) 

  Repeat the 3.3 operation to mark the road surface. Note that just tick the data corresponding to the road surface and click: 

 ![avatar]( 20200127091919667.png) 

 ![avatar]( 20200127091931461.png) 

 ![avatar]( 20200127091944970.png) 

 ![avatar]( 20200127091950925.png) 

 ![avatar]( 20200127092013634.png) 

 ![avatar]( 20200127092027982.png) 

  After labeling, it is observed that: Check all the data, and you can find that the data of different labels will be displayed in different colors: Here, only the data of two labels can be combined and displayed, and 3.2 and 3.3 operations can be performed multiple times before merging: Click the Merge Multiple clouds button to merge: Get a data: Here, you can find that there is an error in the labeling of the building part. The solution refers to Part 5. It is recommended to ensure that each category of data annotation is accurate before merging different categories of data to avoid adding excess work. 

 ![avatar]( 2020012709222786.png) 

 ![avatar]( 20200127092241513.png) 

 The software may suddenly crash, so after marking for a period of time, pay attention to save, select all Ctrl keys, and click the save button. Save type ASCII: Get the above two pieces of data: 

 ![avatar]( 2020012709230774.png) 

 ![avatar]( 2020012709232087.png) 

 ![avatar]( 20200127092329952.png) 

  The last column in Notepad is labeled: Re-import these two data: Select the data that has been annotated, set Colors to Scalar field, and set Active to #7 to observe the display results of the data with different labels. 

 ![avatar]( 20200127092347115.png) 

  Repeat the above steps until all the data annotations are completed and merged into one data. 

 The data might be as shown in the image above, with Colors set to the Scalar field and Active set to #7. 

##  IV. Label the video 

 Link: https://pan.baidu.com/s/1qs9UPtXP0r7E6Z9m2F9A7g Extraction code: vygu 

##  Fives. Error resolution 

 Mark a tree, but the lawn section at the bottom of the tree is also selected. 

 ![avatar]( 20200127102602539.png) 

 ![avatar]( 20200127102608588.png) 

  Follow step 3.2 to cut out the lawn section at the bottom of the tree to obtain:  

 Delete the wrong label information in the lawn section Edit - > Scalar fields - > Delete, the Count of Scalar fields is changed from 7 to the initial 6: 

 ![avatar]( 20200127102614857.png) 

 ![avatar]( 20200127102621726.png) 

 ![avatar]( 20200127102629702.png) 

  Re-label the lawn part and repeat the labeling step 3.3: The lawn belongs to others, enter 0: It is observed that the label has been distinguished: 

 ![avatar]( 20200127102635345.png) 

##  VI. Precautions 

##  VII. Visualization 

 ![avatar]( 2020012710341533.png) 

