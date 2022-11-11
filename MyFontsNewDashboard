import React, { Component } from 'react';
import { ReactiveBase, ReactiveList, SingleList } from '@appbaseio/reactivesearch';
import './App.css';

const tagList = {
  'Grotesque Sans': 'grotesque sans',
  'Blackletter': 'blackletter',
  'Humanist Sans': 'humanist sans',
  'Informal Script': 'informal script',
  'Formal Script': 'formal script',
  'Transitional Serif': 'transitional serif',
  'Modern Serif': 'modern serif',
  'Old Style': 'old style serif',
  'Clarendon Serif': 'clarendon serif',
  'Slab Serif': 'slab serif',
  'Geometric Sans': 'geometric sans',
  'Display': 'display',
  'Symbol': 'symbol',
  "Casual": "casual",
  "Playful":"playful",
  "Techno":"techno",
  "Legible":"legible",
  "Elegant":"elegant",
  "Decorative":"decorative",
  "Industrial":"industrial",
  "Retro":"retro",
  "Romantic":"romantic",
  "Serif":"serif",
  "SansSerif":"sans serif",
  "Stencil":"stencil",
  "Brush":"brush",
  "Rounded":"rounded",
  "Typewriter":"typewriter",
  "Inline":"inline",
  "Comic":"comic",
  "Shaded":"shaded",
  "Clean":"clean",
  "ArtDeco":"artdeco",
  "College":"college",
  "Calligraphy":"calligraphy",
  "Kids":"kids",
  "Wedding":"wedding",
  "Futuristic":"futuristic",
  "Graffiti":"graffiti",
};


const customQueries = {
  "old style serif":()=>(
    {
      query: {
          "query": {
              "bool":{
                  "should":[
                    {
                        "exists": {
                          "field": "mltags.italian old style serif"
                        }
                    },
                    {
                      "exists": {
                        "field": "mltags.french old style serif"
                      }
                    },
                    {
                      "exists": {
                        "field": "mltags.dutch old style serif"
                      }
                    }
                  ]
              }

          }
      },
      size:1000
  }),
//  "clean":()=>(
  //  {
    //  query: {
      //    "query": {
        //      "bool":{
          //        "should":[
            //          {
              //            "bool": {
                //              "must": [
                  //                {
                    //                  "exists": {
                      //                    "field": "mltags.legible"
                        //              }
                          //        },
                            //      {
                              //        "exists": {
                                //          "field": "mltags.geometric sans"
                                  //    }
//                                  }
  //                            ]
    //                      }
      //                },
        //              {
          //                "bool": {
            //                  "must": [
              //                    {
                //                      "exists": {
                  //                        "field": "mltags.legible"
                    //                  }
                      //            },
                        //          {
                          //            "exists": {
                            //              "field": "mltags.grotesque sans"
                              //        }
                                //  }
                  //            ]
                 //         }
//                      }
  //                ]
    //          }
  //
    //      }
//      },
//      size:1000
//  }),
  "friendly":()=>(
    {
      query: {
          "query": {
              "bool":{
                  "should":[
                      {
                          "bool": {
                              "must": [
                                  {
                                      "exists": {
                                          "field": "mltags.playful"
                                      }
                                  },
                                  {
                                      "exists": {
                                          "field": "mltags.casual"
                                      }
                                  }
                              ]
                          }
                      },
                      {
                          "bool": {
                              "must": [
                                  {
                                      "exists": {
                                          "field": "mltags.humanist sans"
                                      }
                                  }
                              ]
                          }
                      },
                      {
                          "bool": {
                              "must": [
                                  {
                                      "exists": {
                                          "field": "mltags.informal script"
                                      }
                                  }
                              ]
                          }
                      }
                  ]
              }

          }
      },
      size:1000
  }),
  "fun": () => ({
    query: {
      "query": {
        "exists": {
          "field": "mltags.playful"
        }
      }
    },
    size:1000
  }),
  "funky":() => ({
    query: {
      "query": {
        "exists": {
          "field": "mltags.decorative"
        }
      }
    },

    size:1000
  }),
  //"futuristic":() => ({
  //  query: {
    //  "query": {
      //  "bool": {
        //    "should": [{
          //      "exists": {
            //        "field":  "mltags.techno"
             //   }
           // },
           // {
             //   "exists": {
               //     "field": "mltags.industrial"
               // }
           // }
           // ]
       // }
   // }
   // },
   // size:1000
 // }),
  "luxury":() => ({
    query: {
      "query": {
        "bool": {
            "should": [{
                "exists": {
                    "field":  "mltags.modern serif"
                }
            },
            {
                "exists": {
                    "field": "mltags.elegant"
                }
            }
            ]
        }
    }
    },
    size:1000
  }),
  "ornament":() => ({
    query: {
      "query": {
        "bool": {
            "should": [{
                "exists": {
                    "field":  "mltags.decorative"
                }
            },
            {
                "exists": {
                    "field": "mltags.symbol"
                }
            }
            ]
        }
    }
    },
    size:1000
  }),
  "rough":() => ({
    query: {
      "query": {
        "bool": {
            "must": [{
                "exists": {
                    "field":  "mltags.industrial"
                }
            },
            {
                "exists": {
                    "field": "mltags.decorative"
                }
            }
            ]
        }
    }
    },
    size:1000
  }),
  "school":() => ({
    query: {
      "query": {
        "bool": {
            "must": [{
                "exists": {
                    "field":  "mltags.informal script"
                }
            },
            {
                "exists": {
                    "field": "mltags.casual"
                }
            }
            ]
        }
    }
    },
    size:1000
  })
};

function get_confidence(item, selectedTag)
  {

      for(const tag in item["mltags"]){
      if (Object.keys(item.mltags[tag])[0] === selectedTag){
          return item.mltags[tag][selectedTag].toFixed(2)
      }
    }
  }


class App extends Component {
  constructor(props) {
    super(props);

    this.handleTagChange = this.handleTagChange.bind(this);
    //this.pangrams = [
    //  'aeiougrqj THOADQGJ wizards pluck ivy from the big quilt.',
    //];
    this.pangrams = [
      'The QUICK quick brown fox jumps over the lazy dog',
    ];
    this.pangramsforCalligraphy = ["The QUICK quick brown fox jumps over the lazy dog"];
    this.pangramsforWedding = ["The QUICK quick brown fox jumps over the lazy dog"];
    const urlParams = new URLSearchParams(window.location.search);
    const myParam = urlParams.get('filtered_fonts_list');
    let indexName = urlParams.get('index_name');
    //if (myParam == 'artdeco' && indexName == 'autotagger-cp'){
    //    indexName = 'autotagger-shaded';}
   // if (myParam == 'college' && indexName == 'autotagger-cp'){
//      indexName = 'autotagger-experiments2';}

  //  console.log("myParam",myParam)
    if (myParam){
      console.log("myParam",myParam)
      this.setState({ selectedTag: myParam});
    }
    if (indexName){
      console.log("myIndex",indexName)
      this.setState({ selectedIndex: indexName});
    }
    this.state = {
      selectedTag: myParam,
      selectedIndex: indexName
    };
  }


  get_final_rank(arr){
    // if(label=="")
    // return arr
    const data = [...arr]
    console.log("length : ",data.length);
    for(var i=0;i<data.length;i++){
        console.log(data[i]);
    }
    data.forEach(function(element){
      if (element.sales && element.sales.bestsellersrank ==null ) {
        element.sales.bestsellersrank = 500000;
      }
  })
    data.sort (function(a,b) {
      if(a.sales == null || b.sales ==null)
      {
        return 0
      }
    return a.sales.bestsellersrank - b.sales.bestsellersrank;
    })
    .forEach (function(d,i) {
      d.bestseller_rank = i+1;
      });
    const { selectedTag } = this.state;

    data.sort (function(a,b) {
    return get_confidence(b,selectedTag) - get_confidence(a,selectedTag);
    }).forEach (function(d,i) {
      d.confidence_rank = i+1;
    });
// // merge two ranking HM cal culate finaly ranking
    arr.forEach(function(element){
      element.final_rank = Number((2/( (1/element.confidence_rank) + ( 1/element.bestseller_rank ) )).toFixed(2));
    })

    arr.sort (function(a,b) {
      return a.final_rank-b.final_rank;
      }).forEach (function(d,i) {
        d.sortFinalRank = i+1;
      });

    // console.log("harmonic mean",)
    // arr.forEach(function(element){
            // console.log("final_rank  = ",element.final_rank,"sort_final_rnk ",element.sortFinalRank,"familyname ",element.familyname)
          // })
    return arr
  }


  handleTagChange(changeEvent) {
    if ('URLSearchParams' in window) {
      var searchParams = new URLSearchParams(window.location.search);
      searchParams.set("filtered_fonts_list", changeEvent.target.value);
      window.location.search = searchParams.toString();
  }
    this.setState({ selectedTag: changeEvent.target.value});
  }

  renderTagFilter() {

    const { selectedTag } = this.state;
    return (
      <div className='sidebar'>
        <h3>AutoTagger V3 </h3>
        {
          Object.keys(tagList).splice(24,10  ).map((key) => (
            <div className='individual-tag' key={`${key} tag`}>
              <input
                type='radio'
                name='tag-list'
                id={tagList[key]}
                value={tagList[key]}
                checked={selectedTag === tagList[key]}
                onChange={this.handleTagChange}
                className='tag-btn'
              />
              <label htmlFor={tagList[key]} className='tag-label'>{key}</label>
              <br />
            </div>
          ))
        }
        <h3>Classification</h3>
        {
          Object.keys(tagList).splice(0,13).map((key) => (
            <div className='individual-tag' key={`${key} tag`}>
              <input
                type='radio'
                name='tag-list'
                id={tagList[key]}
                value={tagList[key]}
                checked={selectedTag === tagList[key]}
                onChange={this.handleTagChange}
                className='tag-btn'
              />
              <label htmlFor={tagList[key]} className='tag-label'>{key}</label>
              <br />
            </div>
          ))
        }
        <h3>AutoTagger V2</h3>
        {
          Object.keys(tagList).splice(13,11).map((key) => (
            <div className='individual-tag' key={`${key} tag`}>
              <input
                type='radio'
                name='tag-list'
                id={tagList[key]}
                value={tagList[key]}
                checked={selectedTag === tagList[key]}
                onChange={this.handleTagChange}
                className='tag-btn'
              />
              <label htmlFor={tagList[key]} className='tag-label'>{key}</label>
              <br />
            </div>
          ))
        }
        <h3>AutoTagger V4 </h3>
        {
          Object.keys(tagList).splice(34,15  ).map((key) => (
            <div className='individual-tag' key={`${key} tag`}>
              <input
                type='radio'
                name='tag-list'
               id={tagList[key]}
                value={tagList[key]}
                checked={selectedTag === tagList[key]}
                onChange={this.handleTagChange}
                className='tag-btn'
              />
              <label htmlFor={tagList[key]} className='tag-label'>{key}</label>
            <br />
            </div>
          ))
        }
      </div>
    );
  }
  renderFonList(item, index){
    var md5hashForImage;
    if(item.language===undefined){
    md5hashForImage = "#und";
    }else{
    md5hashForImage = item.language.md5hash;
    }
    const { selectedTag } = this.state;
    console.log(selectedTag)
    let confidence = 0;
    let ConfidenceString = ""
    for(const tag in item["mltags"]){
      ConfidenceString += Object.keys(item.mltags[tag])[0] +": " + item.mltags[tag][Object.keys(item.mltags[tag])[0]].toFixed(2).toString() +"\n"
    }
    for(const tag in item["mltags"]){
      //console.log(Object.keys(item.mltags[tag])[0])
      if (Object.keys(item.mltags[tag])[0] === selectedTag){
          confidence = item.mltags[tag][selectedTag].toFixed(2)
      }
    }
      item.confidence = confidence
    var isCalligraphy = selectedTag=="calligraphy"
    var isWedding = selectedTag=="wedding"
    return <div className='font-item'>
        <div className='arrow'>
          <span className="numberCircle"><span>{index + 1} </span></span>&nbsp;
        </div>
        {/* <a className='font-name'  target="_blank" href={`https://www.myfonts.com${item.familyurl}`}>{item.familyname}</a> */}
        {/* <a className='font-name'  target="_blank" href={`https://www.myfonts.com${item.familyurl}`}>{item.familyname}</a> */}
        <div className='font-preview'>
          {isCalligraphy || isWedding ?
          <img
            src={`https://render.myfonts.net/fonts/font_rend.php?id=${md5hashForImage}&rt=${this.pangramsforWedding[index % this.pangramsforWedding.length]}&rs=200&bg=ffffff&fg=000000&t=og`}
            alt='Font'
            className='font-image'
          />
          : <img
            src={`https://render.myfonts.net/fonts/font_rend.php?id=${md5hashForImage}&rt=${this.pangrams[index % this.pangrams.length]}&rs=200&bg=ffffff&fg=000000&t=og`}
            alt='Font'
            className='font-image'
          />}
        </div>
        {/* <div className='confidence'>
          {ConfidenceString}
        </div> */ }
      </div>
  }



  render() {
    const { selectedTag, selectedIndex } = this.state;

    let elasticQuery = () => ({
      query: {
        "query": {
          "exists": {
            "field": "mltags."+selectedTag
          }
        }
      }
            //,
      //size:1000
    })
   // if (selectedIndex == "autotagger-post_release"){
//          delete customQueries['clean'];
//          console.log(customQueries);
  //  }
    if (selectedTag in customQueries){
      elasticQuery =  customQueries[selectedTag]
    }
   // let url_direct = 'http://ec2-3-92-58-208.compute-1.amazonaws.com:9200';
    let url_direct='http://ec2-54-152-53-80.compute-1.amazonaws.com:9200';
    console.log(selectedIndex, selectedTag, "#######");
    console.log(elasticQuery);
  //  if (selectedTag == 'college' && selectedIndex == 'autotagger-experiments2'){
  //      url_direct='http://ec2-54-152-53-80.compute-1.amazonaws.com:9200'
  //  }

    return (
      <div className='App'>
        <header className='App-header'>
          <img src='/mt-logo.png' className='App-logo' alt='logo' />
          <h1 className='main-heading'>
            Auto-classifier demo.
          </h1>
        </header>
        {this.renderTagFilter()}
        <ReactiveBase
          app={selectedIndex}
          url={url_direct}
        >
          <SingleList componentId="CitySensor" dataField="mltags.display.keyword" title="Cities"
          renderItem={(label, count, isSelected) => (
            <div>
              {console.log("here")}
                {label}
                <span style={{
                    marginLeft: 5, color: isSelected ? 'red' : 'dodgerblue'
                }}>
                    {count}
                </span>
            </div>
        )}
        renderNoResults={() => <p>No Results Found!</p>}
         />
          <ReactiveList
            URLParams={true}
            componentId='filtered_fonts_list'
            dataField='name'
            includeFields={[
              'language.md5hash','familyurl','familyname',
              'sales.bestsellersrank',
              'mltags'
            ]}
            react={{
              and: ["CitySensor"]
            }}
            scrollOnChange
            render={({ data }) => this.get_final_rank(data).map((item, index) => this.renderFonList(item, index))}
            defaultQuery={elasticQuery}
            size={10000}

            showResultStats={false}
            className='result-list'
          />
        </ReactiveBase>
      </div>
    );
  }
}

export default App;
