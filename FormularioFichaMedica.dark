import 'dart:typed_data';
import 'package:flutter/material.dart';
import 'package:image_picker/image_picker.dart';
import 'package:pdf/pdf.dart';
import 'package:pdf/widgets.dart' as pw;
import 'package:printing/printing.dart';
import 'package:signature/signature.dart';
import 'dart:async';
import 'package:flutter/services.dart';
import 'package:flutter_datetime_picker/flutter_datetime_picker.dart';

class MyForm extends StatefulWidget {
  @override
  _MyFormState createState() => _MyFormState();


}

class _MyFormState extends State<MyForm> {
  final GlobalKey<FormState> _formKey = GlobalKey<FormState>();
  //A
  String _insti = '';
  String _ruc = '';
  String _ciiu = '';
  String _estsalud = '';
  String _numhc = '';
  String _numar = '';
  String _papell = '';
  String _sapell = '';
  String _pnom = '';
  String _snom = '';
  String _sex = '';
  String _puest = '';
  //B
  DateTime? _selectedDate;
  String _eval = '';
  //C
  String _obs = '';
  String _cali = '';
  Uint8List? _imageBytes;

  String _selectedItem = '';
  SignatureController _signatureController = SignatureController(
    penStrokeWidth: 5,
    penColor: Colors.black,
    exportBackgroundColor: Colors.white,
  );

  @override
  Widget build(BuildContext context) {
    Completer<Uint8List> completer = Completer<Uint8List>();
    return Scaffold(
      appBar: AppBar(
        title: Text('Ficha Medica'),
      ),
      body: Form(
        key: _formKey,
        child: ListView(
          padding: EdgeInsets.all(10),
          children: [

            Container(
              decoration: BoxDecoration(
                border: Border.all(
                  color: Colors.black,
                  width: 2,
                ),
              ),
              child: Text(
                'A. DATOS DEL ESTABLECIMIENTO - EMPRESA Y USUARIO',
                style: TextStyle(
                  fontWeight: FontWeight.bold,
                  fontSize: 20,
                ),
              ),
            ),

            TextFormField(
              decoration: InputDecoration(labelText: 'INSTITUCIÓN DEL SISTEMA O NOMBRE DE LA EMPRESA'),
              validator: (String? value) {
                if (value == null || value.trim().isEmpty) {
                  return 'Requerido';
                }
                return null;
              },
              onSaved: (String? value) {
                if (value != null) {
                  _insti = value;
                }
              },
            ),
            TextFormField(
              decoration: InputDecoration(labelText: 'RUC'),

              onSaved: (String? value) {
                if (value != null) {
                  _ruc = value;
                }
              },
            ),
            TextFormField(
              decoration: InputDecoration(labelText: 'CIIU'),

              onSaved: (String? value) {
                if (value != null) {
                  _ciiu = value;
                }
              },
            ),
            TextFormField(
              decoration: InputDecoration(labelText: 'ESTABLECIMIENTO DE SALUD'),

              onSaved: (String? value) {
                if (value != null) {
                  _ciiu = value;
                }
              },
            ),
            TextFormField(
              decoration: InputDecoration(labelText: 'NÚMERO DE HISTORIA CLÍNICA'),

              onSaved: (String? value) {
                if (value != null) {
                  _numhc = value;
                }
              },
            ),
            TextFormField(
              decoration: InputDecoration(labelText: 'NÚMERO ARCHIVO'),

              onSaved: (String? value) {
                if (value != null) {
                  _numar = value;
                }
              },
            ),
            TextFormField(
              decoration: InputDecoration(labelText: 'PRIMER APELLIDO'),

              onSaved: (String? value) {
                if (value != null) {
                  _papell = value;
                }
              },
            ),
            TextFormField(
              decoration: InputDecoration(labelText: 'SEGUNDO APELLIDO'),

              onSaved: (String? value) {
                if (value != null) {
                  _sapell = value;
                }
              },
            ),
            TextFormField(
              decoration: InputDecoration(labelText: 'PRIMER NOMBRE'),

              onSaved: (String? value) {
                if (value != null) {
                  _pnom = value;
                }
              },
            ),
            TextFormField(
              decoration: InputDecoration(labelText: 'SEGUNDO NOMBRE'),

              onSaved: (String? value) {
                if (value != null) {
                  _snom = value;
                }
              },
            ),

            DropdownButtonFormField<String>(
              decoration: InputDecoration(labelText: 'SEXO'),
              items: ['MASCULINO', 'FEMENINO', 'OTRO']
                  .map((label) => DropdownMenuItem(
                child: Text(label),
                value: label,
              ))
                  .toList(),
              onChanged: (String? newValue) {
                if (newValue != null) {
                  setState(() {
                    _sex = newValue;
                  });
                }
              },
            ),


            SizedBox(height: 10),

            Container(
              decoration: BoxDecoration(
                border: Border.all(
                  color: Colors.black,
                  width: 2,
                ),
              ),
              child: Text(
                'B. DATOS GENERALES',
                style: TextStyle(
                  fontWeight: FontWeight.bold,
                  fontSize: 20,
                ),
              ),
            ),

            DropdownButtonFormField<String>(
              decoration: InputDecoration(labelText: 'EVALUACION'),
              items: ['INGRESO', 'PERIODICO', 'REINTEGRO', 'RETIRO']
                  .map((label) => DropdownMenuItem(
                child: Text(label),
                value: label,
              ))
                  .toList(),
              onChanged: (String? newValue) {
                if (newValue != null) {
                  setState(() {
                    _eval = newValue;
                  });
                }
              },
            ),
            ListTile(
              title: Text('Seleccione Fecha'),
              trailing: Icon(Icons.keyboard_arrow_down),
              onTap: () {
                DatePicker.showDatePicker(
                  context,
                  showTitleActions: true,
                  onConfirm: (date) {
                    setState(() {
                      _selectedDate = date;
                    });
                  },
                  currentTime: _selectedDate ?? DateTime.now(),
                );
              },
              subtitle: _selectedDate == null
                  ? null
                  : Text('Selected date: ${_selectedDate!.toLocal().toIso8601String().substring(0, 10)}'),
            ),
            SizedBox(height: 15),
            Container(
              decoration: BoxDecoration(
                border: Border.all(
                  color: Colors.black,
                  width: 2,
                ),
              ),
              child: Text(
                'C. APTITUD MÉDICA LABORAL',
                style: TextStyle(
                  fontWeight: FontWeight.bold,
                  fontSize: 20,
                ),
              ),
            ),
            SizedBox(height: 15),
            Text('Después de la valoración médica ocupacional se certifica que la persona en mención, es calificada como:'),

            DropdownButtonFormField<String>(
              decoration: InputDecoration(labelText: 'Calificacion'),
              items: ['APTO', 'APTO EN OBSERVACIÓN', 'APTO CON LIMITACIONES', 'NO APTO']
                  .map((label) => DropdownMenuItem(
                child: Text(label),
                value: label,
              ))
                  .toList(),
              onChanged: (String? newValue) {
                if (newValue != null) {
                  setState(() {
                    _cali = newValue;
                  });
                }
              },
            ),
            TextFormField(
              decoration: InputDecoration(
                labelText: 'Observación',
                border: OutlineInputBorder(),
              ),
              maxLines: 5, // Define la cantidad de líneas a mostrar en el TextArea
              keyboardType: TextInputType.multiline, // Habilita el ingreso de múltiples líneas de texto
              onSaved: (String? value) {
                if (value != null) {
                  _obs = value;
                }
              },
            ),


            //BOTONES
            ElevatedButton(
              onPressed: () async {
                // Mostrar diálogo para seleccionar fuente de imagen (galería o cámara)
                showDialog(
                  context: context,
                  builder: (BuildContext context) {
                    return AlertDialog(
                      title: Text('Seleccione origen de la imagen'),
                      actions: [
                        TextButton(
                          onPressed: () async {
                            Navigator.of(context).pop();
                            final picker = ImagePicker();
                            final pickedImage = await picker.getImage(source: ImageSource.gallery);
                            if (pickedImage != null) {
                              // Obtener bytes de la imagen seleccionada
                              final imageBytes = await pickedImage.readAsBytes();
                              // Agregar la imagen al PDF
                              setState(() {
                                _imageBytes = imageBytes;
                              });
                            }
                          },
                          child: Text('Galeria'),
                        ),
                        TextButton(
                          onPressed: () async {
                            Navigator.of(context).pop();
                            final picker = ImagePicker();
                            final pickedImage = await picker.getImage(source: ImageSource.camera);
                            if (pickedImage != null) {
                              // Obtener bytes de la imagen seleccionada
                              final imageBytes = await pickedImage.readAsBytes();
                              // Agregar la imagen al PDF
                              setState(() {
                                _imageBytes = imageBytes;
                              });
                            }
                          },
                          child: Text('Camara'),
                        ),
                      ],
                    );
                  },
                );
              },
              child: Text('Subir Firma Medico'),
            ),

            Container(
              decoration: BoxDecoration(
                borderRadius: BorderRadius.circular(10.0), // Radio de curvatura de las esquinas del borde
                border: Border.all(
                  color: Colors.black, // Color del borde
                  width: 2.0, // Ancho del borde
                ),
              ),
              child: ClipRRect(
                borderRadius: BorderRadius.circular(10.0), // Radio de curvatura de las esquinas del ClipRRect
                child: Signature(
                  controller: _signatureController,
                  height: 200,
                  backgroundColor: Colors.white10,
                ),
              ),
            ),


            SizedBox(height: 16),
            ElevatedButton(
              onPressed: () {
                // Limpiar la firma
                _signatureController.clear();
              },
              child: Text('Reintentar Firma'),
            ),
            SizedBox(height: 16),




            ElevatedButton(
              onPressed: () async {
                if (_formKey.currentState != null &&
                    _formKey.currentState!.validate()) {
                  if (_imageBytes == null || _imageBytes!.isEmpty) {
                    showDialog(
                      context: context,
                      builder: (BuildContext context) {
                        return AlertDialog(
                          title: Text('Error'),
                          content: Text('Debe subir la firma.'),
                          actions: [
                            TextButton(
                              onPressed: () {
                                Navigator.of(context).pop();
                              },
                              child: Text('OK'),
                            ),
                          ],
                        );
                      },
                    );
                    return;
                  }
                  _formKey.currentState!.save();
                  final pdf = pw.Document();

                  // Obtener bytes de la imagen
                  final signatureBytes = await _signatureController.toPngBytes();





// Crear una lista de filas de datos
                  List<List<String>> tableDataA = [
                    [    'Institución del sistema o nombre de la empresa',    'RUC',    'CIIU',    'ESTABLECIMIENTO DE SALUD',    'NÚMERO DE HISTORIA CLÍNICA',    'NÚMERO DE ARCHIVO'  ],
                    [    '$_insti',    '$_ruc',    '$_ciiu',    '$_estsalud',    '$_numhc',    '$_numar'  ],
                    [    'PRIMER APELLIDO ',    'SEGUNDO APELLIDO',    'PRIMER NOMBRE',    'SEGUNDO NOMBRE',    'SEXO',    'PUESTO DE TRABAJO (CIUO)'  ],
                    [    '$_papell',    '$_sapell',    '$_pnom',    '$_snom',    '$_sex',    '$_puest'  ],
                  ];

// Agregar resaltado de filas




// Luego, en tu código existente:
                  pw.Table tableA = pw.Table.fromTextArray(

                    data: tableDataA,

                    headerStyle:pw.TextStyle(fontSize: 8) ,
                    cellStyle: pw.TextStyle(fontSize: 8),
                    border: pw.TableBorder.all(width: 1),
                    cellAlignments: {
                      0: pw.Alignment.center,
                      1: pw.Alignment.center,
                      2: pw.Alignment.center,
                      3: pw.Alignment.center,
                      4: pw.Alignment.center,
                      5: pw.Alignment.center,
                    },

                    cellHeight: 20,

                  );

                  List<List<String>> tableDataB = [
                    [    'FECHA DE EMISION',    'EVALUACION'  ],
                    [    '$_selectedDate',    '$_eval'  ],

                  ];

// Agregar resaltado de filas




// Luego, en tu código existente:
                  pw.Table tableB = pw.Table.fromTextArray(

                    data: tableDataB,

                    headerStyle:pw.TextStyle(fontSize: 8) ,
                    cellStyle: pw.TextStyle(fontSize: 8),
                    border: pw.TableBorder.all(width: 1),
                    cellAlignments: {
                      0: pw.Alignment.center,
                      1: pw.Alignment.center,

                    },

                    cellHeight: 20,

                    ////////////////////////////////////////////////////



                  );
                  //////////////////////////////////////////////

                  List<List<String>> tableDataC = [
                    [    'Después de la valoración médica ocupacional se certifica que la persona en mención, es calificada como:',    '$_cali'  ],
                    [    'DETALLE DE OBSERVACIONES:',    '$_obs'  ],

                  ];

// Agregar resaltado de filas




// Luego, en tu código existente:
                  pw.Table tableC = pw.Table.fromTextArray(

                      data: tableDataC,

                      headerStyle:pw.TextStyle(fontSize: 8) ,
                      cellStyle: pw.TextStyle(fontSize: 8),
                      border: pw.TableBorder.all(width: 1),
                      cellAlignments: {
                        0: pw.Alignment.center,
                        1: pw.Alignment.center,

                      },

                      cellHeight: 20,
                  );
                  ///////////////////////////////////////////////////////////////////////////
                  // Agregar la tabla y otros elementos a la página del PDF
                  pdf.addPage(
                      pw.Page(
                        build: (pw.Context context) => pw.Column(
                            crossAxisAlignment: pw.CrossAxisAlignment.start,
                            children: [
                              pw.Text(
                                'A. DATOS DEL ESTABLECIMIENTO - EMPRESA Y USUARIO',
                                style: pw.TextStyle(fontSize: 10), // Cambiar tamaño de fuente a 20
                              ),
                              tableA,
                              pw.SizedBox(height: 5),
                              pw.Text(
                                'B. DATOS GENERALES ',
                                style: pw.TextStyle(fontSize: 10), // Cambiar tamaño de fuente a 20
                              ),
                              tableB, // Agregar la tabla
                              pw.SizedBox(height: 5),
                              pw.Text(
                                'C. APTITUD MÉDICA LABORAL ',
                                style: pw.TextStyle(fontSize: 10), // Cambiar tamaño de fuente a 20
                              ),
                              tableC,

                      pw.SizedBox(height: 20), // Agregar un espacio vertical entre la tabla y los otros elementos
                      //pw.Text('Agreed to terms and conditions? $_agreedToTerms'),
                      pw.Text('$_selectedItem'),
                      pw.Text('Firma Usuario:'),
                      pw.Image(
                        signatureBytes != null
                            ? pw.MemoryImage(signatureBytes)
                            : pw.MemoryImage(Uint8List(0)), // Usar una lista vacía si signatureBytes es nulo
                        width: 200,
                        height: 100,
                      ),
                      pw.Image(
                        _imageBytes != null
                            ? pw.MemoryImage(_imageBytes!)
                            : pw.MemoryImage(Uint8List(0)), // Usar una lista vacía si _imageBytes es nulo
                        width: 200,
                        height: 100,
                      ),
                    ]),
                  ));

                  await Printing.layoutPdf(
                    onLayout: (PdfPageFormat format) async => pdf.save(),
                  );
                }
              },
              child: Text('Generar'),
            ),





          ],
        ),
      ),
    );
  }
}
