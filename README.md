import React from "react"; 
import FigureList from "./FigureList"; 
import "./App.css"; 
 
function App() { 
  return ( 
    <div className="App"> 
      <h1>Figure List</h1> 
      <FigureList /> 
    </div> 
  ); 
} 
export default App; 


FigureList.js 
import React, { useState } from "react"; 
function BasicFigure ({ image, caption, onRemove })  { 
  return ( 
    <div className="basic-figure"> 
      <img src={image} alt={caption} className="figure-image" /> 
      <figcaption className="figure-caption">{caption}</figcaption> 
      <button className="remove-button" onClick={onRemove}> 
        Remove 
      </button> 
    </div> 
  ); 
} 
 
function FigureList () { 
  const [figures, setFigures] = useState([ 
    { id: 1, image: "https://www.w3schools.com/w3images/lights.jpg", caption: 
"Beautiful Lights" }, 
    { id: 2, image: "https://www.w3schools.com/w3images/nature.jpg", caption: 
"Nature" }, 
  ]); 
  const [newImage, setNewImage] = useState(""); 
  const [newCaption, setNewCaption] = useState(""); 
 
  function addFigure () { 
    if (newImage && newCaption) { 
      setFigures([ 
        ...figures, 
        { id: Date.now(), image: newImage, caption: newCaption } 
      ]); 
      setNewImage(""); 
      setNewCaption(""); 
    } 
  }; 
 
  const removeFigure = (id) => { 
    setFigures(figures.filter((figure) => figure.id !== id)); 
  }; 
 
   return ( 
    <div className="figure-list"> 
      <input 
        type="text" 
        placeholder="Image URL" 
        value={newImage} 
        onChange={(e) => setNewImage(e.target.value)} 
      /> 
      <input 
        type="text" 
        placeholder="Caption" 
        value={newCaption} 
        onChange={(e) => setNewCaption(e.target.value)} 
      /> 
      <button onClick={addFigure}>Add Image</button> 
 
      <div className="simple-grid"> 
        {figures.map((figure) => ( 
          <BasicFigure 
            image={figure.image} 
            caption={figure.caption} 
            onRemove={() => removeFigure(figure.id)} 
          /> 
        ))} 
      </div> 
    </div> 
  ); 
} 
export default FigureList; 


 
App.css 
.App { 
    font-family: Arial, sans-serif; 
    text-align: center; 
    padding: 20px; 
} 
 
.figure-list input { 
    margin: 5px; 
    padding: 8px; 
    width: 180px; 
    border: 1px solid #ccc; 
    border-radius: 4px; 
} 
 
.figure-list button { 
    padding: 8px 12px; 
    background-color: #4caf50; 
    color: white; 
    border: none; 
    border-radius: 4px; 
    cursor: pointer; 
} 
 
    .figure-list button:hover { 
        background-color: #45a049; 
    } 
 
.simple-grid { 
    display: flex; 
    flex-wrap: wrap; 
    justify-content: center; 
    gap: 16px; 
    margin-top: 20px; 
} 
 
.basic-figure { 
    background: #f9f9f9; 
    padding: 10px; 
    border-radius: 10px; 
    width: 160px; 
    position: relative; 
    box-shadow: 0 2px 5px rgba(0, 0, 0, 0.1); 
} 
 
.figure-image { 
    width: 100%; 
    border-radius: 6px; 
    transition: transform 0.3s ease, box-shadow 0.3s ease; 
} 
 
    .figure-image:hover { 
        transform: scale(1.05); 
        box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2); 
    } 
 
.figure-caption { 
    margin-top: 8px; 
    font-size: 14px; 
    color: #444; 
} 
 
.remove-button { 
    position: absolute; 
    top: 5px; 
    right: 5px; 
    background-color: #e74c3c; 
    color: white; 
    border: none; 
    border-radius: 50%; 
    padding: 4px 7px; 
    cursor: pointer; 
    font-size: 12px; 
} 
 
    .remove-button:hover { 
        background-color: #c0392b; 
    } 
 
