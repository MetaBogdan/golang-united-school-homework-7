package coverage

import (
	"github.com/stretchr/testify/assert"
	"os"
	"testing"
	"time"
)

// DO NOT EDIT THIS FUNCTION
func init() {
	content, err := os.ReadFile("students_test.go")
	if err != nil {
		panic(err)
	}
	err = os.WriteFile("autocode/students_test", content, 0644)
	if err != nil {
		panic(err)
	}
}

// WRITE YOUR CODE BELOW

func TestPeopleLen(t *testing.T) {
	t.Parallel()
	testedVal := map[string]People{
		"handred": make(People, 100),
		"empty":   make(People, 0),
		"nil":     nil,
	}
	for name, v := range testedVal {
		people := v
		t.Run(name, func(t *testing.T) {
			t.Parallel()
			assert.Equal(t, people.Len(), len(people))
		})

	}
}

func TestPeopleLess(t *testing.T) {
	t.Parallel()
	people := People{
		Person{firstName: "Alice", lastName: "Sligo", birthDay: time.Date(1981, 11, 11, 0, 0, 0, 0, time.UTC)},
		Person{firstName: "Cristina", lastName: "Zatory", birthDay: time.Date(1983, 12, 12, 0, 0, 0, 0, time.UTC)},
		Person{firstName: "Zarina", lastName: "Avenger", birthDay: time.Date(1981, 11, 11, 0, 0, 0, 0, time.UTC)},
		Person{firstName: "Zarina", lastName: "Wulcano", birthDay: time.Date(1981, 11, 11, 0, 0, 0, 0, time.UTC)},
		Person{firstName: "Marg", lastName: "Simpson", birthDay: time.Date(1981, 11, 11, 0, 0, 0, 0, time.UTC)},
	}
	tData := map[string]struct {
		people   People
		i        int
		j        int
		expected bool
	}{
		"older":                               {people, 0, 1, false},
		"younger":                             {people, 1, 0, true},
		"The same birthday, first name wins":  {people, 0, 2, true},
		"The same birthday, first name loses": {people, 2, 0, false},
		"The same birthday and first name, last name wins":  {people, 2, 3, true},
		"The same birthday and first name, last name loses": {people, 3, 2, false}}

	for name, value := range tData {
		people := value.people
		i := value.i
		j := value.j
		expected := value.expected
		t.Run(name, func(t *testing.T) {
			t.Parallel()
			assert.Equal(t, expected, people.Less(i, j))
		})
	}
}

func TestPeopleSwap(t *testing.T) {
	t.Parallel()
	cristina := Person{firstName: "Cristina", lastName: "Zatory", birthDay: time.Date(1983, 12, 12, 0, 0, 0, 0, time.UTC)}
	zarina := Person{firstName: "Zarina", lastName: "Avenger", birthDay: time.Date(1981, 11, 11, 0, 0, 0, 0, time.UTC)}
	people := People{cristina, zarina}

	people.Swap(0, 1)

	assert.Equalf(t, people[0], zarina, "zarina should be first")
	assert.Equalf(t, people[1], cristina, "cristina should be second")
}

func TestMatrixNewReturnNill(t *testing.T) {
	t.Parallel()
	tableVal := map[string]string{
		"empty":  "",
		"zigzag": "0 1\n0 1 2"}

	for name, value := range tableVal {
		input := value
		t.Run(name, func(t *testing.T) {
			t.Parallel()
			actual, err := New(input)
			assert.NotNil(t, err)
			assert.Nil(t, actual)
		})

	}

}

func TestMatrixNewReturnsNotNil(t *testing.T) {
	t.Parallel()

	tableVal := map[string]struct {
		input string
		rows  int
		cols  int
	}{
		"single row":    {"0 1 2 3", 1, 4},
		"multiple rows": {"0 1 2\n3 4 5\n6 7 8", 3, 3},
		"multiple rows with leading and trailing spaces": {" 0 1 2\n 3 4 5 \n6 7 8 ", 3, 3}}

	for name, value := range tableVal {
		tCase := value
		t.Run(name, func(t *testing.T) {
			t.Parallel()
			actual, err := New(tCase.input)
			assert.Equal(t, tCase.rows, actual.rows)
			assert.Equal(t, tCase.cols, actual.cols)
			assert.Nil(t, err)
			assert.NotNil(t, actual)
			assert.NotNil(t, actual.data)

		})
	}
}

func TestMatrixRows(t *testing.T) {
	t.Parallel()

	tableVal := map[string]struct {
		input string
		rows  [][]int
	}{
		"single row":    {"0 1 2 3", [][]int{{0, 1, 2, 3}}},
		"multiple rows": {"0 1 2\n3 4 5\n6 7 8", [][]int{{0, 1, 2}, {3, 4, 5}, {6, 7, 8}}}}

	for name, value := range tableVal {
		tCase := value
		t.Run(name, func(t *testing.T) {
			t.Parallel()
			matrix, _ := New(tCase.input)
			assert.Equal(t, tCase.rows, matrix.Rows())
		})
	}
}

func TestMatrixCols(t *testing.T) {
	t.Parallel()

	tableVal := map[string]struct {
		input string
		cols  [][]int
	}{
		"single row":    {"0 1 2 3", [][]int{{0}, {1}, {2}, {3}}},
		"multiple rows": {"0 1 2\n3 4 5\n6 7 8", [][]int{{0, 3, 6}, {1, 4, 7}, {2, 5, 8}}}}

	for name, value := range tableVal {
		tCase := value
		t.Run(name, func(t *testing.T) {
			t.Parallel()
			matrix, _ := New(tCase.input)
			assert.Equal(t, tCase.cols, matrix.Cols())
		})
	}
}

func TestMatrixSetFails(t *testing.T) {
	t.Parallel()

	matrix, _ := New("0 1 2")
	tableVal := map[string]struct {
		row int
		col int
	}{
		"negative row":     {-1, 0},
		"row out of range": {1, 0},
		"negative col":     {0, -1},
		"col out of range": {0, 3}}

	for name, value := range tableVal {
		tCase := value
		t.Run(name, func(t *testing.T) {
			t.Parallel()
			assert.False(t, matrix.Set(tCase.row, tCase.col, 100))
		})
	}
}

func TestMatrixSet(t *testing.T) {
	t.Parallel()

	tableVal := map[string]struct {
		input string
		row   int
		col   int
		value int
	}{
		"single row":    {"0 1 2", 0, 1, 3},
		"multiple rows": {"0 1 2\n3 4 5\n6 7 8", 2, 2, 9}}

	for name, value := range tableVal {
		tCase := value
		t.Run(name, func(t *testing.T) {
			t.Parallel()
			matrix, _ := New(tCase.input)
			assert.True(t, matrix.Set(tCase.row, tCase.col, tCase.value))
			assert.Equal(t, tCase.value, matrix.Rows()[tCase.row][tCase.col])
		})
	}
}
