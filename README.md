# TestCase

```import { Component, ChangeEvent } from 'react';

interface Param {
  id: number;
  name: string;
  type: 'string';
}

interface ParamValue {
  paramId: number;
  value: string;
}

interface Model {
  paramValues: ParamValue[];
  colors: string[];
}

interface Props {
  params: Param[];
  model: Model;
}

interface State {
  paramValues: ParamValue[];
}

class ParamEditor extends Component<Props, State> {
  constructor(props: Props) {
    super(props);
    this.state = {
      paramValues: props.model.paramValues
    };
    this.handleParamChange = this.handleParamChange.bind(this);
  }

  getModel(): Model {
    return {
      paramValues: this.state.paramValues,
      colors: this.props.model.colors
    };
  }

  render() {
    return (
      <div>
        {this.props.params.map(param => (
          <div key={param.id}>
            <label>{param.name}</label>
            <input
              type="text"
              value={this.getParamValue(param.id)}
              onChange={(e: ChangeEvent<HTMLInputElement>) =>
                this.handleParamChange(param.id, e.target.value)
              }
            />
          </div>
        ))}
      </div>
    );
  }

  private getParamValue(paramId: number): string {
    const paramValue = this.state.paramValues.find(
      paramValue => paramValue.paramId === paramId
    );
    return paramValue ? paramValue.value : '';
  }

  private handleParamChange(paramId: number, value: string) {
    const updatedParamValues = this.state.paramValues.map(paramValue => {
      if (paramValue.paramId === paramId) {
        return { ...paramValue, value: value };
      }
      return paramValue;
    });

    this.setState({
      paramValues: updatedParamValues
    });
  }
}

export default ParamEditor;```
