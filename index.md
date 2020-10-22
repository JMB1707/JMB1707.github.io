## Welcome Jean Marcos
![Robot](https://www.google.com/search?q=machine+learning&sxsrf=ALeKk01x_MU-RC-c1s9H-uEqeHSPyiEL2Q:1603326762518&source=lnms&tbm=isch&sa=X&ved=2ahUKEwiA2o3R-cbsAhUNwVkKHf4fC8cQ_AUoAXoECAcQAw&biw=1365&bih=694#imgrc=LKzHSnM7xxhexM.jpg)

### AIOS
Un sistema operativo de inteligencia artificial (AIOS) es una forma de software del sistema que administra los recursos de hardware y software de la computadora y proporciona servicios comunes para programas de computadora a través de la inteligencia artificial general. El sistema operativo AI es un componente del software del sistema en un sistema informático.
### Tipos de sistemas operativos de IA
### Impreso
Los primeros sistemas operativos de IA para lograr el éxito técnico y en el mercado masivo utilizaron una forma de impresión cerebral que copiaba con precisión la red neuronal / conectoma de un cerebro. Estos tipos de AIOS se restringieron en las décadas de 70 y 80 y se prohibieron en 2006, sin embargo, formaron la base de los primeros programas y sistemas operativos autocorregibles. Durante la Tercera Guerra Mundial e incluso después de la prohibición de la mayoría de los AIOS impresos se crearon a partir de cerebros de animales, más comúnmente insectos, ratas, ratones y monos. Estos AIOS impresos rudimentarios continúan utilizándose para robots simples encargados de labores domésticas y tareas de custodia civil. La prohibición fue finalmente derogada por la 35ª Enmienda.
### Con plantilla
Los AIOS basados en plantillas son anteriores a los sistemas operativos impresos, pero no se utilizaron de forma masiva después de la prohibición de la IA impresa en 2108. El software AIOS basado en plantillas se crea mediante codificación rígida y programación algorítmica de redes neuronales. Estos programas contienen menos instancias de "lógica difusa" en el código profundo y, por lo tanto, no son capaces de lograr sensibilidad. Se utilizan una serie de algoritmos genéticos en una simulación cuántica para crear una IA útil sometiéndola a una variedad de pruebas y condiciones diferentes. Muchos de estos AIOS se compilaron a partir de cachés de datos y algoritmos binarios existentes.

### Machine Learning
El Aprendizaje Automático consiste en una disciplina de las ciencias informáticas, relacionada con el desarrollo de la Inteligencia Artificial, y que sirve, como ya se ha dicho, para crear sistemas que pueden aprender por sí solos.
Es una tecnología que permite hacer automáticas una serie de operaciones con el fin de reducir la necesidad de que intervengan los seres humanos. Esto puede suponer una gran ventaja a la hora de controlar una ingente cantidad de información de un modo mucho más efectivo.
### Cómo funciona el Machine Learning
En la informática clásica, el único modo de conseguir que un sistema informático hiciera algo era escribiendo un algoritmo que definiera el contexto y detalles de cada acción.

En cambio, los algoritmos que se usan en el desarrollo del Machine Learning realizan buena parte de estas acciones por su cuenta. Obtienen sus propios cálculos según los datos que se recopilan en el sistema, y cuantos más datos obtienen, mejores y más precisas serán las acciones resultantes.





<script src="https://www.gstatic.com/dialogflow-console/fast/messenger/bootstrap.js?v=1"></script>
<df-messenger
  chat-title="Terminos_SO"
  agent-id="d5cde31f-b52b-49d8-b76b-8eb798aaf712"
  language-code="es"
></df-messenger>


<div>Teachable Machine Image Model</div>
<button type="button" onclick="init()">Start</button>
<div id="webcam-container"></div>
<div id="label-container"></div>
<script src="https://cdn.jsdelivr.net/npm/@tensorflow/tfjs@1.3.1/dist/tf.min.js"></script>
<script src="https://cdn.jsdelivr.net/npm/@teachablemachine/image@0.8/dist/teachablemachine-image.min.js"></script>
<script type="text/javascript">
    // More API functions here:
    // https://github.com/googlecreativelab/teachablemachine-community/tree/master/libraries/image

    // the link to your model provided by Teachable Machine export panel
    const URL = "https://teachablemachine.withgoogle.com/models/ambnQ0wmI/";

    let model, webcam, labelContainer, maxPredictions;

    // Load the image model and setup the webcam
    async function init() {
        const modelURL = URL + "model.json";
        const metadataURL = URL + "metadata.json";

        // load the model and metadata
        // Refer to tmImage.loadFromFiles() in the API to support files from a file picker
        // or files from your local hard drive
        // Note: the pose library adds "tmImage" object to your window (window.tmImage)
        model = await tmImage.load(modelURL, metadataURL);
        maxPredictions = model.getTotalClasses();

        // Convenience function to setup a webcam
        const flip = true; // whether to flip the webcam
        webcam = new tmImage.Webcam(200, 200, flip); // width, height, flip
        await webcam.setup(); // request access to the webcam
        await webcam.play();
        window.requestAnimationFrame(loop);

        // append elements to the DOM
        document.getElementById("webcam-container").appendChild(webcam.canvas);
        labelContainer = document.getElementById("label-container");
        for (let i = 0; i < maxPredictions; i++) { // and class labels
            labelContainer.appendChild(document.createElement("div"));
        }
    }

    async function loop() {
        webcam.update(); // update the webcam frame
        await predict();
        window.requestAnimationFrame(loop);
    }

    // run the webcam image through the image model
    async function predict() {
        // predict can take in an image, video or canvas html element
        const prediction = await model.predict(webcam.canvas);
        for (let i = 0; i < maxPredictions; i++) {
            const classPrediction =
                prediction[i].className + ": " + prediction[i].probability.toFixed(2);
            labelContainer.childNodes[i].innerHTML = classPrediction;
        }
    }
</script>

